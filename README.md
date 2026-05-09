Starting program: /usr/apps/com.samsung.tv.cobalt/bin/cobalt_launcher
warning: File "/usr/lib/libthread_db.so.1" auto-loading has been declined by your `auto-load safe-path' set to "$debugdir:$datadir/auto-load".
To enable execution of this file add
        add-auto-load-safe-path /usr/lib/libthread_db.so.1
line to your configuration file "/root/.gdbinit".
To completely disable this security protection add
        set auto-load safe-path /
line to your configuration file "/root/.gdbinit".
For more information about this security protection see the
"Auto-loading safe path" section in the GDB manual.  E.g., run from the shell:
        info "(gdb)Auto-loading safe path"
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
[New LWP 17304]
[17286:17286:19700101,095449.329928:INFO crashpad_client_linux.cc:333] Added evergreen info: --evergreen-information=0x5a8960
[17286:17286:19700101,095449.332394:INFO crashpad_client_linux.cc:96] Added annotation: --annotation=user_agent_string=Mozilla/5.0 (Tizen; /6.0/2025.30.1034943) Cobalt/25.lts.30.1034943-qa (unlike Gecko) v8/8.8.278.17-jit gles Evergreen/5.30.2 Evergreen-Full Evergreen-Compressed Starboard/16, Samsung_TV_PONTUSM_2021/T-NKM2AKUC (Samsung, QAQ80)
[New LWP 17306]
[New LWP 17307]
[New LWP 17308]
[New LWP 17309]
[New LWP 17311]
[New LWP 17310]
[New LWP 17312]
[New LWP 17313]
[17286:17286:19700101,095449.346179:INFO crashpad_client_linux.cc:85] Updated annotation: --annotation=user_agent_string=Mozilla/5.0 (Tizen; /6.0/2025.30.1034943) Cobalt/25.lts.30.1034943-qa (unlike Gecko) v8/8.8.278.17-jit gles Evergreen/5.30.2 Evergreen-Full Evergreen-Compressed Starboard/16, Samsung_TV_PONTUSM_2021/T-NKM2AKUC (Samsung, QAQ80)
[New LWP 17314]
[17286:17286:19700101,095449.346826:INFO crashpad_client_linux.cc:85] Updated annotation: --annotation=prod=Cobalt_Evergreen
[17286:17286:19700101,095449.347012:INFO crashpad_client_linux.cc:85] Updated annotation: --annotation=ver=5.30.2
[New LWP 17315]
[New LWP 17316]
[New LWP 17317]
[New LWP 17318]

(process:17286): GLib-CRITICAL **: 09:54:49.372: '(iislu)' is not a valid GVariant format string

(process:17286): GLib-CRITICAL **: 09:54:49.373: g_variant_new: assertion 'valid_format_string (format_string, TRUE, NULL) && format_string[0] != '?' && format_string[0] != '@' && format_string[0] != '*' && format_string[0] != 'r'' failed
[New LWP 17319]
[New LWP 17320]
[New LWP 17321]
[New LWP 17336]
[New LWP 17337]
[New LWP 17338]

Thread 21 "Rasterizer" received signal SIGSEGV, Segmentation fault.
[Switching to LWP 17338]
0xaf446f90 in ?? ()
(gdb) thread apply all bt

Thread 21 (LWP 17338):
#0  0xaf446f90 in ?? ()
#1  0xaf655b10 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

