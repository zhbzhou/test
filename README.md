The program being debugged has been started already.
Start it from the beginning? (y or n) y
Starting program: /usr/apps/com.samsung.tv.cobalt/bin/cobalt_launcher
warning: File "/usr/lib/libthread_db.so.1" auto-loading has been declined by your `auto-load safe-path' set to "$                                                                                                                                                                       debugdir:$datadir/auto-load".
warning: Unable to find libthread_db matching inferior's thread library, thread debugging will not be available.
Traceback (most recent call last):
  File "/usr/share/gdb/auto-load/usr/lib/libgstreamer-1.0.so.0.2411.0-gdb.py", line 9, in <module>
    from gst_gdb import register
  File "/usr/share/gstreamer-1.0/gdb/gst_gdb.py", line 26, in <module>
    from glib_gobject_helper import g_type_to_name, g_type_name_from_instance, \
  File "/usr/share/gstreamer-1.0/gdb/glib_gobject_helper.py", line 96
    return gdb.parse_and_eval(f"g_type_name({gtype})").string()
                                                    ^
SyntaxError: invalid syntax
pthread_create called
#0  __pthread_create_2_1 (newthread=0x5a41d0, attr=0x0,
    start_routine=0x445da4 <starboard::Thread::ThreadEntryPoint(void*)>,
    arg=0x56d848 <starboard::shared::signal::ConfigureSignalHandlerThread(bool)::handlerThread>)
    at pthread_create.c:632
#1  0x00445e6c in starboard::Thread::Start() ()
#2  0x00472cd0 in StandAloneMain(int, char**) ()
#3  0x00410108 in main ()
[New LWP 29048]
[29032:29032:19700102,075440.616252:INFO crashpad_client_linux.cc:333] Added evergreen info: --evergreen-informat                                                                                                                                                                       ion=0x5a8960
[29032:29032:19700102,075440.618110:INFO crashpad_client_linux.cc:96] Added annotation: --annotation=user_agent_s                                                                                                                                                                       tring=Mozilla/5.0 (Tizen; /6.0/2025.30.1034943) Cobalt/25.lts.30.1034943-qa (unlike Gecko) v8/8.8.278.17-jit gles                                                                                                                                                                        Evergreen/5.30.2 Evergreen-Full Evergreen-Compressed Starboard/16, Samsung_TV_PONTUSM_2021/T-NKM2AKUC (Samsung,                                                                                                                                                                        QAQ80)
pthread_create called
#0  __pthread_create_2_1 (newthread=0xbeffdf0c, attr=0xbeffdf10, start_routine=0xaec086f4, arg=0x5ba3b8)
    at pthread_create.c:632
#1  0x00414518 in __abi_wrap_pthread_create ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)
[New LWP 29050]
pthread_create called
#0  __pthread_create_2_1 (newthread=0xbeffde34, attr=0xbeffde38, start_routine=0xaec086f4, arg=0x5ba590)
    at pthread_create.c:632
#1  0x00414518 in __abi_wrap_pthread_create ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)
[New LWP 29051]
pthread_create called
#0  __pthread_create_2_1 (newthread=0xbeffdf5c, attr=0xbeffdf60, start_routine=0xaec086f4, arg=0x5bc240)
    at pthread_create.c:632
#1  0x00414518 in __abi_wrap_pthread_create ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)
[New LWP 29052]
pthread_create called
#0  __pthread_create_2_1 (newthread=0x5bf750, attr=0x0, start_routine=0xaefb061c, arg=0x5bf6a0)
    at pthread_create.c:632
#1  0x00414518 in __abi_wrap_pthread_create ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)
[New LWP 29053]
[Switching to LWP 29051]
pthread_create called
#0  __pthread_create_2_1 (newthread=0xb0ffe584, attr=0xb0ffe588, start_routine=0xaec086f4, arg=0xb0600868)
    at pthread_create.c:632
#1  0x00414518 in __abi_wrap_pthread_create ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)
[Switching to LWP 29032]
pthread_create called
#0  __pthread_create_2_1 (newthread=0xbeffdf5c, attr=0xbeffdf60, start_routine=0xaec086f4, arg=0x5db208)
    at pthread_create.c:632
#1  0x00414518 in __abi_wrap_pthread_create ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)
[New LWP 29054]
[New LWP 29055]
[Switching to LWP 29055]
pthread_create called
#0  __pthread_create_2_1 (newthread=0xb11d4e8c, attr=0xb11d4e90, start_routine=0xaec086f4, arg=0xafb05150)
    at pthread_create.c:632
#1  0x00414518 in __abi_wrap_pthread_create ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)
[New LWP 29056]
[Switching to LWP 29032]
pthread_create called
#0  __pthread_create_2_1 (newthread=0xbeffdf5c, attr=0xbeffdf60, start_routine=0xaec086f4, arg=0x5d1c60)
    at pthread_create.c:632
#1  0x00414518 in __abi_wrap_pthread_create ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)
[New LWP 29057]
[29032:29032:19700102,075440.707070:INFO crashpad_client_linux.cc:85] Updated annotation: --annotation=user_agent                                                                                                                                                                       _string=Mozilla/5.0 (Tizen; /6.0/2025.30.1034943) Cobalt/25.lts.30.1034943-qa (unlike Gecko) v8/8.8.278.17-jit gl                                                                                                                                                                       es Evergreen/5.30.2 Evergreen-Full Evergreen-Compressed Starboard/16, Samsung_TV_PONTUSM_2021/T-NKM2AKUC (Samsung                                                                                                                                                                       , QAQ80)
[29032:29032:19700102,075440.707177:INFO crashpad_client_linux.cc:85] Updated annotation: --annotation=prod=Cobal                                                                                                                                                                       t_Evergreen
[29032:29032:19700102,075440.707249:INFO crashpad_client_linux.cc:85] Updated annotation: --annotation=ver=5.30.2
--Type <RET> for more, q to quit, c to continue without paging--
[Switching to LWP 29057]
pthread_create called
#0  __pthread_create_2_1 (newthread=0xabcd826c, attr=0xabcd8270, start_routine=0xaec086f4, arg=0xaf902ba0) at pthread_create.c:632
#1  0x00414518 in __abi_wrap_pthread_create ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)
[Switching to LWP 29032]
pthread_create called
#0  __pthread_create_2_1 (newthread=0xbeffdf2c, attr=0xbeffdf30, start_routine=0xaec086f4, arg=0x5d9618) at pthread_create.c:632
#1  0x00414518 in __abi_wrap_pthread_create ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)
[New LWP 29099]
[New LWP 29100]
pthread_create called
#0  __pthread_create_2_1 (newthread=0xbeffde14, attr=0xbeffde18, start_routine=0xaec086f4, arg=0x5d16c8) at pthread_create.c:632
#1  0x00414518 in __abi_wrap_pthread_create ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)
[New LWP 29101]
[Switching to LWP 29101]
pthread_create called
#0  __pthread_create_2_1 (newthread=0xaa4d5254, attr=0xaa4d5258, start_routine=0xaec086f4, arg=0xaf804bd0) at pthread_create.c:632
#1  0x00414518 in __abi_wrap_pthread_create ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)
[New LWP 29102]
pthread_create called
#0  __pthread_create_2_1 (newthread=0xaa4d51bc, attr=0xaa4d51c0, start_routine=0xaec086f4, arg=0xaf805948) at pthread_create.c:632
#1  0x00414518 in __abi_wrap_pthread_create ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)
[New LWP 29103]
[Switching to LWP 29032]
pthread_create called
#0  __pthread_create_2_1 (newthread=0x6083b8, attr=0xbeffda30, start_routine=0xb60d0509, arg=0x608398) at pthread_create.c:632
#1  0xb60f2706 in ?? () from /lib/libglib-2.0.so.0
#2  0xb60d08f4 in g_thread_new () from /lib/libglib-2.0.so.0
#3  0xb60d11be in g_thread_pool_new_full () from /lib/libglib-2.0.so.0
#4  0xb60d12c8 in g_thread_pool_new () from /lib/libglib-2.0.so.0
#5  0xb5a5a512 in ?? () from /lib/libgio-2.0.so.0
#6  0xb5a5a830 in g_task_get_type () from /lib/libgio-2.0.so.0
#7  0xb5aabdb2 in ?? () from /lib/libgio-2.0.so.0
#8  0xb5aa20e8 in g_bus_get_sync () from /lib/libgio-2.0.so.0
#9  0xb6281430 in __dbus_get_connection () at /usr/src/debug/resource-center-api-0.1-1.arm/src/resource_center_private.cpp:105
#10 0xb628175a in __dbus_method_call (method=method@entry=0xb62880f8 "RscChangeRegId", args=0x604d40, result=result@entry=0xbeffdc20) at /usr/src/debug/resource-center-api-0.1-1.arm/src/resource_center_private.cpp:129
#11 0xb6284142 in _rc_register_resource_change_callback_app_id (app_id=app_id@entry=0x5814f8 "com.samsung.tv.cobalt-yt", func=func@entry=0x483c2c <MediaConfig::OnResourceChanged(char const*, rc_resource*, void*)>)
    at /usr/src/debug/resource-center-api-0.1-1.arm/src/resource_center_private.cpp:1481
#12 0xb6285b78 in _rc_register_resource_change_callback (app_id=0x5814f8 "com.samsung.tv.cobalt-yt", cb=0x483c2c <MediaConfig::OnResourceChanged(char const*, rc_resource*, void*)>, data=<optimized out>)
    at /usr/src/debug/resource-center-api-0.1-1.arm/src/resource_center_private.cpp:1564
#13 0x00484fcc in MediaConfig::SetResourceChangeCB(void (*)(void*), void*) ()
#14 0x004db364 in starboard::tizen::product::ApplicationTizen::CreateWindow(SbWindowOptions const*) ()
#15 0xaf106628 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)
[New LWP 29105]
pthread_create called
#0  __pthread_create_2_1 (newthread=0x608628, attr=0xbeffd950, start_routine=0xb60d0509, arg=0x608608) at pthread_create.c:632
#1  0xb60f2706 in ?? () from /lib/libglib-2.0.so.0
#2  0xb60d08f4 in g_thread_new () from /lib/libglib-2.0.so.0
#3  0xb60b2120 in ?? () from /lib/libglib-2.0.so.0
#4  0xb5a5a55c in ?? () from /lib/libgio-2.0.so.0
#5  0xb5a5a830 in g_task_get_type () from /lib/libgio-2.0.so.0
#6  0xb5aabdb2 in ?? () from /lib/libgio-2.0.so.0
#7  0xb5aa20e8 in g_bus_get_sync () from /lib/libgio-2.0.so.0
#8  0xb6281430 in __dbus_get_connection () at /usr/src/debug/resource-center-api-0.1-1.arm/src/resource_center_private.cpp:105
#9  0xb628175a in __dbus_method_call (method=method@entry=0xb62880f8 "RscChangeRegId", args=0x604d40, result=result@entry=0xbeffdc20) at /usr/src/debug/resource-center-api-0.1-1.arm/src/resource_center_private.cpp:129
#10 0xb6284142 in _rc_register_resource_change_callback_app_id (app_id=app_id@entry=0x5814f8 "com.samsung.tv.cobalt-yt", func=func@entry=0x483c2c <MediaConfig::OnResourceChanged(char const*, rc_resource*, void*)>)
    at /usr/src/debug/resource-center-api-0.1-1.arm/src/resource_center_private.cpp:1481
#11 0xb6285b78 in _rc_register_resource_change_callback (app_id=0x5814f8 "com.samsung.tv.cobalt-yt", cb=0x483c2c <MediaConfig::OnResourceChanged(char const*, rc_resource*, void*)>, data=<optimized out>)
    at /usr/src/debug/resource-center-api-0.1-1.arm/src/resource_center_private.cpp:1564
#12 0x00484fcc in MediaConfig::SetResourceChangeCB(void (*)(void*), void*) ()
#13 0x004db364 in starboard::tizen::product::ApplicationTizen::CreateWindow(SbWindowOptions const*) ()
#14 0xaf106628 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)
[New LWP 29106]
pthread_create called
#0  __pthread_create_2_1 (newthread=0x5e3768, attr=0xbeffdaa8, start_routine=0xb60d0509, arg=0x5e3748) at pthread_create.c:632
#1  0xb60f2706 in ?? () from /lib/libglib-2.0.so.0
#2  0xb60d08f4 in g_thread_new () from /lib/libglib-2.0.so.0
#3  0xb5aabafa in ?? () from /lib/libgio-2.0.so.0
#4  0xb5aa0d84 in ?? () from /lib/libgio-2.0.so.0
#5  0xb5aa2104 in g_bus_get_sync () from /lib/libgio-2.0.so.0
#6  0xb6281430 in __dbus_get_connection () at /usr/src/debug/resource-center-api-0.1-1.arm/src/resource_center_private.cpp:105
#7  0xb628175a in __dbus_method_call (method=method@entry=0xb62880f8 "RscChangeRegId", args=0x604d40, result=result@entry=0xbeffdc20) at /usr/src/debug/resource-center-api-0.1-1.arm/src/resource_center_private.cpp:129
#8  0xb6284142 in _rc_register_resource_change_callback_app_id (app_id=app_id@entry=0x5814f8 "com.samsung.tv.cobalt-yt", func=func@entry=0x483c2c <MediaConfig::OnResourceChanged(char const*, rc_resource*, void*)>)
    at /usr/src/debug/resource-center-api-0.1-1.arm/src/resource_center_private.cpp:1481
#9  0xb6285b78 in _rc_register_resource_change_callback (app_id=0x5814f8 "com.samsung.tv.cobalt-yt", cb=0x483c2c <MediaConfig::OnResourceChanged(char const*, rc_resource*, void*)>, data=<optimized out>)
    at /usr/src/debug/resource-center-api-0.1-1.arm/src/resource_center_private.cpp:1564
#10 0x00484fcc in MediaConfig::SetResourceChangeCB(void (*)(void*), void*) ()
#11 0x004db364 in starboard::tizen::product::ApplicationTizen::CreateWindow(SbWindowOptions const*) ()
#12 0xaf106628 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)
[New LWP 29107]
pthread_create called
#0  __pthread_create_2_1 (newthread=0x5fcc00, attr=0xbeffda30, start_routine=0xb60d0509, arg=0x5fcbe0) at pthread_create.c:632
--Type <RET> for more, q to quit, c to continue without paging--
#1  0xb60f2706 in ?? () from /lib/libglib-2.0.so.0
#2  0xb60d08f4 in g_thread_new () from /lib/libglib-2.0.so.0
#3  0xb078ca66 in tpl_gthread_create () from /lib/libtpl-egl.so.1
#4  0xb0791fac in ?? () from /lib/libtpl-egl.so.1
#5  0xb0789ffc in tpl_display_create () from /lib/libtpl-egl.so.1
#6  0xb07c8706 in dri2_initialize_tizen (disp=disp@entry=0x5e9ab8) at ../src/egl/drivers/dri2/platform_tizen.c:1442
#7  0xb07c660c in dri2_initialize (disp=0x5e9ab8) at ../src/egl/drivers/dri2/egl_dri2.c:930
#8  dri2_initialize (disp=0x5e9ab8) at ../src/egl/drivers/dri2/egl_dri2.c:883
#9  0xb07b83d6 in eglInitialize (dpy=<optimized out>, major=0x0, minor=0x0) at ../src/egl/main/eglapi.c:722
#10 0xaf2b2a88 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)
[New LWP 29136]
pthread_create called
#0  __pthread_create_2_1 (newthread=newthread@entry=0x6047f0, attr=attr@entry=0x0, start_routine=0xa6c36ef5 <impl_thrd_routine>, arg=arg@entry=0x606678) at pthread_create.c:632
#1  0xa6c37162 in thrd_create (thr=0x6047f0, func=0xa6c1f801 <util_queue_thread_func>, arg=0x5d0bb0) at ../src/c11/impl/threads_posix.c:254
#2  0xa6c20198 in u_thread_create (thrd=0x6047f0, routine=0xa6c1f801 <util_queue_thread_func>, param=param@entry=0x5d0bb0) at ../src/util/u_thread.c:66
#3  0xa6c1f752 in util_queue_create_thread (queue=queue@entry=0x60e5e8, index=index@entry=0) at ../src/util/u_queue.c:328
#4  0xa6c1fe7e in util_queue_init (queue=queue@entry=0x60e5e8, name=<optimized out>, max_jobs=max_jobs@entry=32, num_threads=num_threads@entry=4, flags=flags@entry=7, global_data=0x0) at ../src/util/u_queue.c:454
#5  0xa6c136e0 in disk_cache_init_queue (cache=0x60e5e0) at ../src/util/disk_cache.c:89
#6  disk_cache_init_queue (cache=0x60e5e0) at ../src/util/disk_cache.c:74
#7  disk_cache_type_create (gpu_name=gpu_name@entry=0x60d940 "V3D 4.2.14.0", driver_id=driver_id@entry=0xbeffd118 "e4bb450697e3cfc58c71339e1ebbb9b44c0fdbd8", driver_flags=<optimized out>, cache_type=DISK_CACHE_DATABASE) at ../src/util/disk_cache.c:213
#8  0xa6c1380c in disk_cache_create (gpu_name=0x60d940 "V3D 4.2.14.0", driver_id=driver_id@entry=0xbeffd118 "e4bb450697e3cfc58c71339e1ebbb9b44c0fdbd8", driver_flags=<optimized out>) at ../src/util/disk_cache.c:286
#9  0xa6e1e9f0 in v3d_disk_cache_init (screen=screen@entry=0x60d198) at ../src/gallium/drivers/v3d/v3d_disk_cache.c:65
#10 0xa6e1d318 in v3d_screen_create (fd=57, config=0xbeffd228, ro=<optimized out>) at ../src/gallium/drivers/v3d/v3d_screen.c:988
#11 0xa6e1be22 in u_pipe_screen_lookup_or_create (gpu_fd=57, config=config@entry=0xbeffd228, ro=ro@entry=0x5fc388, screen_create=0xa6e1d1a9 <v3d_screen_create>) at ../src/gallium/auxiliary/util/u_screen.c:687
#12 0xa6dede4a in v3d_drm_screen_create_renderonly (fd=<optimized out>, ro=ro@entry=0x5fc388, config=config@entry=0xbeffd228) at ../src/gallium/winsys/v3d/drm/v3d_drm_winsys.c:45
#13 0xa6deddc2 in kmsro_drm_screen_create (kms_fd=kms_fd@entry=55, config=config@entry=0xbeffd228) at ../src/gallium/winsys/kmsro/drm/kmsro_drm_winsys.c:113
#14 0xa6dede90 in vc4_drm_screen_create (fd=55, config=0xbeffd228) at ../src/gallium/winsys/vc4/drm/vc4_drm_winsys.c:56
#15 0xa68b4a4a in pipe_vc4_create_screen (fd=<optimized out>, config=<optimized out>) at ../src/gallium/auxiliary/target-helpers/drm_helper.h:305
#16 0xa6dd35c2 in pipe_loader_create_screen_vk (dev=0x5fd258, sw_vk=sw_vk@entry=false, driver_name_is_inferred=<optimized out>) at ../src/gallium/auxiliary/pipe-loader/pipe_loader.c:181
#17 0xa6dd35f0 in pipe_loader_create_screen (dev=<optimized out>, driver_name_is_inferred=<optimized out>) at ../src/gallium/auxiliary/pipe-loader/pipe_loader.c:187
#18 0xa68bafa0 in dri2_init_screen (screen=screen@entry=0x5fc6b8, driver_name_is_inferred=driver_name_is_inferred@entry=false) at ../src/gallium/frontends/dri/dri2.c:2004
#19 0xa68b7604 in driCreateNewScreen3 (scrn=scrn@entry=0, fd=<optimized out>, loader_extensions=0xb07f2428 <tizen_dri2_loader_extensions>, type=type@entry=DRI_SCREEN_DRI3, driver_configs=driver_configs@entry=0x5ea518, driver_name_is_inferred=driver_name_is_inferred@entry=false,
    has_multibuffer=has_multibuffer@entry=true, data=data@entry=0x5e9ab8) at ../src/gallium/frontends/dri/dri_util.c:138
#20 0xb07c5fe6 in dri2_create_screen (disp=disp@entry=0x5e9ab8) at ../src/egl/drivers/dri2/egl_dri2.c:825
#21 0xb07c874e in dri2_initialize_tizen (disp=disp@entry=0x5e9ab8) at ../src/egl/drivers/dri2/platform_tizen.c:1533
#22 0xb07c660c in dri2_initialize (disp=0x5e9ab8) at ../src/egl/drivers/dri2/egl_dri2.c:930
#23 dri2_initialize (disp=0x5e9ab8) at ../src/egl/drivers/dri2/egl_dri2.c:883
#24 0xb07b83d6 in eglInitialize (dpy=<optimized out>, major=0x0, minor=0x0) at ../src/egl/main/eglapi.c:722
#25 0xaf2b2a88 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)
[New LWP 29137]
pthread_create called
#0  __pthread_create_2_1 (newthread=0xbeffdc1c, attr=0xbeffdc20, start_routine=0xaec086f4, arg=0x18158b0) at pthread_create.c:632
#1  0x00414518 in __abi_wrap_pthread_create ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)
[New LWP 29139]

Thread 21 "Rasterizer" received signal SIGSEGV, Segmentation fault.
[Switching to LWP 29139]
0xaf446f90 in ?? ()
(gdb)
