Pipeline::Pipeline(const CreateRasterizerFunction& create_rasterizer_function,
                   const scoped_refptr<backend::RenderTarget>& render_target,
                   backend::GraphicsContext* graphics_context,
                   bool submit_even_if_render_tree_is_unchanged,
                   ShutdownClearMode clear_on_shutdown_mode,
                   const Options& options)
    : rasterizer_created_event_(
          base::WaitableEvent::ResetPolicy::MANUAL,
          base::WaitableEvent::InitialState::NOT_SIGNALED),
      render_target_(render_target),
      graphics_context_(graphics_context),
      rasterizer_thread_("Rasterizer"),
      submission_disposal_thread_("RasterzrSubDisp"),
      submit_even_if_render_tree_is_unchanged_(
          submit_even_if_render_tree_is_unchanged),
      last_did_rasterize_(false),
      last_animations_expired_(true),
      last_stat_tracked_animations_expired_(true),
      rasterize_animations_timer_("Renderer.Rasterize.Animations",
                                  kRasterizeAnimationsTimerMaxEntries,
                                  true /*enable_entry_list_c_val*/),
      ALLOW_THIS_IN_INITIALIZER_LIST(rasterize_periodic_interval_timer_(
          "Renderer.Rasterize.DurationInterval",
          kRasterizeAnimationsTimerMaxEntries, true /*enable_entry_list_c_val*/,
          base::Bind(&Pipeline::FrameStatsOnFlushCallback,
                     base::Unretained(this)))),
      rasterize_animations_interval_timer_(
          "Renderer.Rasterize.AnimationsInterval",
          kRasterizeAnimationsTimerMaxEntries,
          true /*enable_entry_list_c_val*/),
      new_render_tree_rasterize_count_(
          "Count.Renderer.Rasterize.NewRenderTree", 0,
          "Total number of new render trees rasterized."),
      new_render_tree_rasterize_time_(
          "Time.Renderer.Rasterize.NewRenderTree", 0,
          "The last time a new render tree was rasterized."),
      has_active_animations_c_val_(
          "Renderer.HasActiveAnimations", false,
          "Is non-zero if the current render tree has active animations."),
      animations_start_time_(
          "Time.Renderer.Rasterize.Animations.Start", 0,
          "The most recent time animations started playing."),
      animations_end_time_("Time.Renderer.Rasterize.Animations.End", 0,
                           "The most recent time animations ended playing."),
      fallback_rasterize_count_(
          "Count.Renderer.Rasterize.FallbackRasterize", 0,
          "Total number of times Skia was used to render a "
          "non-text render tree node."),
#if defined(ENABLE_DEBUGGER)
      ALLOW_THIS_IN_INITIALIZER_LIST(dump_current_render_tree_command_handler_(
          "dump_render_tree",
          base::Bind(&Pipeline::OnDumpCurrentRenderTree,
                     base::Unretained(this)),
          "Dumps the current render tree to text.",
          "Dumps the current render tree either to the console if no parameter "
          "is specified, or to a file with the specified filename relative to "
          "the debug output folder.")),
      ALLOW_THIS_IN_INITIALIZER_LIST(toggle_fps_stdout_command_handler_(
          "toggle_fps_stdout",
          base::Bind(&Pipeline::OnToggleFpsStdout, base::Unretained(this)),
          "Toggles printing framerate stats to stdout.",
          "When enabled, at the end of each animation (or every time a maximum "
          "number of frames are rendered), framerate statistics are printed "
          "to stdout.")),
      ALLOW_THIS_IN_INITIALIZER_LIST(toggle_fps_overlay_command_handler_(
          "toggle_fps_overlay",
          base::Bind(&Pipeline::OnToggleFpsOverlay, base::Unretained(this)),
          "Toggles rendering framerate stats to an overlay on the display.",
          "Framerate statistics are rendered to a display overlay.  The "
          "numbers are updated at the end of each animation (or every time a "
          "maximum number of frames are rendered), framerate statistics are "
          "printed to stdout.")),
#endif  // defined(ENABLE_DEBUGGER)
      clear_on_shutdown_mode_(clear_on_shutdown_mode),
      enable_fps_stdout_(options.enable_fps_stdout),
      enable_fps_overlay_(options.enable_fps_overlay),
      fps_overlay_update_pending_(false) {

  TRACE_EVENT0("cobalt::renderer", "Pipeline::Pipeline()");
  // The actual Pipeline can be constructed from any thread, but we want
  // rasterizer_thread_checker_ to be associated with the rasterizer thread,
  // so we detach it here and let it reattach itself to the rasterizer thread
  // when CalledOnValidThread() is called on rasterizer_thread_checker_ below.
  DETACH_FROM_THREAD(rasterizer_thread_checker_);
  rasterizer_thread_.StartWithOptions(
      base::Thread::Options(base::ThreadType::kMaxValue));

  rasterizer_thread_.task_runner()->PostTask(
      FROM_HERE,
      base::Bind(&Pipeline::InitializeRasterizerThread, base::Unretained(this),
                 create_rasterizer_function));
}