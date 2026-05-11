Type "apropos word" to search for commands related to "word"...
Reading symbols from /usr/apps/com.samsung.tv.cobalt/bin/cobalt_launcher...
Reading symbols from /usr/lib/debug/usr/apps/com.samsung.tv.cobalt/bin/cobalt_launcher.debug...
(gdb) r
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
[New LWP 13918]
[13889:13889:19700103,060707.918297:INFO crashpad_client_linux.cc:333] Added evergreen info: --evergreen-information=0x5a8960
[13889:13889:19700103,060707.919769:INFO crashpad_client_linux.cc:96] Added annotation: --annotation=user_agent_string=Mozilla/5.0 (Tizen; /6.0/2025.30.1034943) Cobalt/25.lts.30.1034943-qa (unlike Gecko) v8/8.8.278.17-jit gles Evergreen/5.30.2 Evergreen-Full Evergreen-Compressed Starboard/16, Samsung_TV_PONTUSM_2021/T-NKM2AKUC (Samsung, QAQ80)
[New LWP 13920]
[New LWP 13921]
[New LWP 13922]
[New LWP 13923]
[New LWP 13925]
[New LWP 13924]
[New LWP 13926]
[New LWP 13927]
[13889:13889:19700103,060707.932649:INFO crashpad_client_linux.cc:85] Updated annotation: --annotation=user_agent_string=Mozilla/5.0 (Tizen; /6.0/2025.30.1034943) Cobalt/25.lts.30.1034943-qa (unlike Gecko) v8/8.8.278.17-jit gles Evergreen/5.30.2 Evergreen-Full Evergreen-Compressed Starboard/16, Samsung_TV_PONTUSM_2021/T-NKM2AKUC (Samsung, QAQ80)
[13889:13889:19700103,060707.932708:INFO crashpad_client_linux.cc:85] Updated annotation: --annotation=prod=Cobalt_Evergreen
[13889:13889:19700103,060707.932736:INFO crashpad_client_linux.cc:85] Updated annotation: --annotation=ver=5.30.2
[New LWP 13928]
[New LWP 13929]
[New LWP 13930]
[New LWP 13931]
[New LWP 13932]
[New LWP 13933]
[New LWP 13934]
[New LWP 13935]
[New LWP 13950]
[New LWP 13951]
[New LWP 13952]

Thread 21 "Rasterizer" received signal SIGSEGV, Segmentation fault.
[Switching to LWP 13952]
0xaf446f90 in ?? ()
(gdb) bt
#0  0xaf446f90 in ?? ()
#1  0xaf655b10 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)
(gdb) thread apply all bt

Thread 21 (LWP 13952):
#0  0xaf446f90 in ?? ()
#1  0xaf655b10 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 20 (LWP 13951):
#0  0xb5b8d6f8 in __futex_abstimed_wait_common32 (private=<optimized out>, futex_word=<optimized out>, expected=<optimized out>, op=<optimized out>, abstime=<optimized out>, cancel=<optimized out>) at futex-internal.c:40
#1  __futex_abstimed_wait_common (futex_word=0x5f6560, futex_word@entry=0xa749e344 <pthread_cond_wait@got.plt>, expected=2784704420, expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=0, private@entry=6251832, cancel=cancel@entry=true) at futex-internal.c:99
#2  0xb5b8d838 in __GI___futex_abstimed_wait_cancelable64 (futex_word=futex_word@entry=0xa749e344 <pthread_cond_wait@got.plt>, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=private@entry=0) at futex-internal.c:139
#3  0xb5b901bc in __pthread_cond_wait_common (cond=0x5f6538, mutex=0x5f6560, clockid=0, abstime=0x0) at pthread_cond_wait.c:503
#4  ___pthread_cond_wait (cond=0x5f6538, mutex=0x5f6560) at pthread_cond_wait.c:618
#5  0xa6c7c21a in cnd_wait (cond=<optimized out>, mtx=<optimized out>) at ../src/c11/impl/threads_posix.c:111
#6  0xa6c63148 in util_queue_thread_func (input=<optimized out>) at ../src/util/u_queue.c:275
#7  0xb5b90eac in start_thread (arg=0xa5fb3e60) at pthread_create.c:447
#8  0xb5c0048c in ?? () at ../sysdeps/unix/sysv/linux/arm/clone3.S:71 from /lib/libc.so.6
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 19 (LWP 13950):
#0  0xb5bf5a18 in __GI___poll (fds=0x616f10, nfds=7, timeout=-1) at ../sysdeps/unix/sysv/linux/poll.c:29
#1  __GI___poll (fds=0x616f10, nfds=7, timeout=-1) at ../sysdeps/unix/sysv/linux/poll.c:26
#2  0xb60b1278 in ?? () from /lib/libglib-2.0.so.0
#3  0xb60b182e in g_main_loop_run () from /lib/libglib-2.0.so.0
#4  0xafdb36e6 in ?? () from /lib/libtpl-egl.so.1
#5  0xb60d0532 in ?? () from /lib/libglib-2.0.so.0
#6  0xb5b90eac in start_thread (arg=0xa68f5e60) at pthread_create.c:447
#7  0xb5c0048c in ?? () at ../sysdeps/unix/sysv/linux/arm/clone3.S:71 from /lib/libc.so.6
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 18 (LWP 13935):
#0  0xb5bf5a18 in __GI___poll (fds=0x60fe98, nfds=2, timeout=-1) at ../sysdeps/unix/sysv/linux/poll.c:29
#1  __GI___poll (fds=0x60fe98, nfds=2, timeout=-1) at ../sysdeps/unix/sysv/linux/poll.c:26
#2  0xb60b1278 in ?? () from /lib/libglib-2.0.so.0
#3  0xb60b182e in g_main_loop_run () from /lib/libglib-2.0.so.0
#4  0xb5aab20a in ?? () from /lib/libgio-2.0.so.0
#5  0xb60d0532 in ?? () from /lib/libglib-2.0.so.0
#6  0xb5b90eac in start_thread (arg=0xa7cd0e60) at pthread_create.c:447
#7  0xb5c0048c in ?? () at ../sysdeps/unix/sysv/linux/arm/clone3.S:71 from /lib/libc.so.6
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 17 (LWP 13934):
#0  0xb5bf5a18 in __GI___poll (fds=0xb0601c88, nfds=1, timeout=-1) at ../sysdeps/unix/sysv/linux/poll.c:29
#1  __GI___poll (fds=0xb0601c88, nfds=1, timeout=-1) at ../sysdeps/unix/sysv/linux/poll.c:26
#2  0xb60b1278 in ?? () from /lib/libglib-2.0.so.0
#3  0xb60b164c in g_main_context_iteration () from /lib/libglib-2.0.so.0
#4  0xb60b1674 in ?? () from /lib/libglib-2.0.so.0
#5  0xb60d0532 in ?? () from /lib/libglib-2.0.so.0
#6  0xb5b90eac in start_thread (arg=0xa84d1e60) at pthread_create.c:447
#7  0xb5c0048c in ?? () at ../sysdeps/unix/sysv/linux/arm/clone3.S:71 from /lib/libc.so.6
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 16 (LWP 13933):
#0  syscall () at ../sysdeps/unix/sysv/linux/arm/syscall.S:37
#1  0xb60f29d4 in g_cond_wait () from /lib/libglib-2.0.so.0
#2  0xb6089626 in ?? () from /lib/libglib-2.0.so.0
#3  0xb60d0b20 in ?? () from /lib/libglib-2.0.so.0
#4  0xb60d0532 in ?? () from /lib/libglib-2.0.so.0
#5  0xb5b90eac in start_thread (arg=0xa8cd2e60) at pthread_create.c:447
#6  0xb5c0048c in ?? () at ../sysdeps/unix/sysv/linux/arm/clone3.S:71 from /lib/libc.so.6
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 15 (LWP 13932):
#0  0xb5b8d6f8 in __futex_abstimed_wait_common32 (private=<optimized out>, futex_word=<optimized out>, expected=<optimized out>, op=<optimized out>, abstime=<optimized out>, cancel=<optimized out>) at futex-internal.c:40
#1  __futex_abstimed_wait_common (futex_word=0xa94d358c, futex_word@entry=0xaebd8314, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=0, private@entry=-1454557852, cancel=cancel@entry=true) at futex-internal.c:99
#2  0xb5b8d838 in __GI___futex_abstimed_wait_cancelable64 (futex_word=futex_word@entry=0xaebd8314, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=private@entry=0) at futex-internal.c:139
#3  0xb5b901bc in __pthread_cond_wait_common (cond=0xa94d3564, mutex=0xa94d358c, clockid=0, abstime=0x0) at pthread_cond_wait.c:503
#4  ___pthread_cond_wait (cond=0xa94d3564, mutex=0xa94d358c) at pthread_cond_wait.c:618
#5  0x004140c8 in __abi_wrap_pthread_cond_wait ()
#6  0xaec06318 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 14 (LWP 13931):
#0  0xb5b8d6f8 in __futex_abstimed_wait_common32 (private=<optimized out>, futex_word=<optimized out>, expected=<optimized out>, op=<optimized out>, abstime=<optimized out>, cancel=<optimized out>) at futex-internal.c:40
#1  __futex_abstimed_wait_common (futex_word=0xa9cd458c, futex_word@entry=0x0, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=0, private@entry=-1446165148, cancel=cancel@entry=true) at futex-internal.c:99
#2  0xb5b8d838 in __GI___futex_abstimed_wait_cancelable64 (futex_word=futex_word@entry=0x0, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=private@entry=0) at futex-internal.c:139
#3  0xb5b901bc in __pthread_cond_wait_common (cond=0xa9cd4564, mutex=0xa9cd458c, clockid=0, abstime=0x0) at pthread_cond_wait.c:503
#4  ___pthread_cond_wait (cond=0xa9cd4564, mutex=0xa9cd458c) at pthread_cond_wait.c:618
#5  0x004140c8 in __abi_wrap_pthread_cond_wait ()
#6  0xaec06318 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

--Type <RET> for more, q to quit, c to continue without paging--
Thread 13 (LWP 13930):
#0  0xb5b8d6f8 in __futex_abstimed_wait_common32 (private=<optimized out>, futex_word=<optimized out>, expected=<optimized out>, op=<optimized out>, abstime=<optimized out>, cancel=<optimized out>) at futex-internal.c:40
#1  __futex_abstimed_wait_common (futex_word=0xaa4d5594, futex_word@entry=0xaf6f6670, expected=expected@entry=0, clockid=clockid@entry=-1437772520, abstime=abstime@entry=0x0, private=0, private@entry=-1437772436, cancel=cancel@entry=true) at futex-internal.c:99
#2  0xb5b8d838 in __GI___futex_abstimed_wait_cancelable64 (futex_word=futex_word@entry=0xaf6f6670, expected=expected@entry=0, clockid=clockid@entry=-1437772520, abstime=abstime@entry=0x0, private=0, private@entry=2042) at futex-internal.c:139
#3  0xb5b90514 in __pthread_cond_wait_common (cond=0xaa4d556c, mutex=0x0, clockid=-1437772520, abstime=<optimized out>) at pthread_cond_wait.c:503
#4  ___pthread_cond_timedwait64 (cond=0xaa4d556c, mutex=0x0, abstime=<optimized out>) at pthread_cond_wait.c:643
#5  0xb5b90614 in ___pthread_cond_timedwait (cond=<optimized out>, mutex=<optimized out>, abstime=<optimized out>) at pthread_cond_wait.c:658
#6  0x00413ebc in __abi_wrap_pthread_cond_timedwait ()
#7  0xaec063f8 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 12 (LWP 13929):
#0  0xb5c00ab4 in epoll_wait (epfd=39, events=0xaf803248, maxevents=32, timeout=30000) at ../sysdeps/unix/sysv/linux/epoll_wait.c:30
#1  0x0050fd84 in epoll_dispatch ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 11 (LWP 13928):
#0  0xb5b8d6f8 in __futex_abstimed_wait_common32 (private=<optimized out>, futex_word=<optimized out>, expected=<optimized out>, op=<optimized out>, abstime=<optimized out>, cancel=<optimized out>) at futex-internal.c:40
#1  __futex_abstimed_wait_common (futex_word=0xab4d758c, futex_word@entry=0xaebd8314, expected=33152, expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=0, private@entry=-1420987036, cancel=cancel@entry=true) at futex-internal.c:99
#2  0xb5b8d838 in __GI___futex_abstimed_wait_cancelable64 (futex_word=futex_word@entry=0xaebd8314, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=private@entry=0) at futex-internal.c:139
#3  0xb5b901bc in __pthread_cond_wait_common (cond=0xab4d7564, mutex=0xab4d758c, clockid=0, abstime=0x0) at pthread_cond_wait.c:503
#4  ___pthread_cond_wait (cond=0xab4d7564, mutex=0xab4d758c) at pthread_cond_wait.c:618
#5  0x004140c8 in __abi_wrap_pthread_cond_wait ()
#6  0xaec06318 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 10 (LWP 13927):
#0  0xb5b8d6f8 in __futex_abstimed_wait_common32 (private=<optimized out>, futex_word=<optimized out>, expected=<optimized out>, op=<optimized out>, abstime=<optimized out>, cancel=<optimized out>) at futex-internal.c:40
#1  __futex_abstimed_wait_common (futex_word=0xabcd858c, futex_word@entry=0xaebd8314, expected=43, expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=0, private@entry=-1412594332, cancel=cancel@entry=true) at futex-internal.c:99
#2  0xb5b8d838 in __GI___futex_abstimed_wait_cancelable64 (futex_word=futex_word@entry=0xaebd8314, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=private@entry=0) at futex-internal.c:139
#3  0xb5b901bc in __pthread_cond_wait_common (cond=0xabcd8564, mutex=0xabcd858c, clockid=0, abstime=0x0) at pthread_cond_wait.c:503
#4  ___pthread_cond_wait (cond=0xabcd8564, mutex=0xabcd858c) at pthread_cond_wait.c:618
#5  0x004140c8 in __abi_wrap_pthread_cond_wait ()
#6  0xaec06318 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 9 (LWP 13926):
#0  0xb5b8d6f8 in __futex_abstimed_wait_common32 (private=<optimized out>, futex_word=<optimized out>, expected=<optimized out>, op=<optimized out>, abstime=<optimized out>, cancel=<optimized out>) at futex-internal.c:40
#1  __futex_abstimed_wait_common (futex_word=0xac4d958c, futex_word@entry=0xaebd8314, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=0, private@entry=-1404201628, cancel=cancel@entry=true) at futex-internal.c:99
#2  0xb5b8d838 in __GI___futex_abstimed_wait_cancelable64 (futex_word=futex_word@entry=0xaebd8314, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=private@entry=0) at futex-internal.c:139
#3  0xb5b901bc in __pthread_cond_wait_common (cond=0xac4d9564, mutex=0xac4d958c, clockid=0, abstime=0x0) at pthread_cond_wait.c:503
#4  ___pthread_cond_wait (cond=0xac4d9564, mutex=0xac4d958c) at pthread_cond_wait.c:618
#5  0x004140c8 in __abi_wrap_pthread_cond_wait ()
#6  0xaec06318 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 8 (LWP 13924):
#0  0xb5b8d6f8 in __futex_abstimed_wait_common32 (private=<optimized out>, futex_word=<optimized out>, expected=<optimized out>, op=<optimized out>, abstime=<optimized out>, cancel=<optimized out>) at futex-internal.c:40
#1  __futex_abstimed_wait_common (futex_word=0xaccda634, futex_word@entry=0x0, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=0, private@entry=-1395808756, cancel=cancel@entry=true) at futex-internal.c:99
#2  0xb5b8d838 in __GI___futex_abstimed_wait_cancelable64 (futex_word=futex_word@entry=0x0, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=private@entry=0) at futex-internal.c:139
#3  0xb5b901bc in __pthread_cond_wait_common (cond=0xaccda60c, mutex=0xaccda634, clockid=0, abstime=0x0) at pthread_cond_wait.c:503
#4  ___pthread_cond_wait (cond=0xaccda60c, mutex=0xaccda634) at pthread_cond_wait.c:618
#5  0x004140c8 in __abi_wrap_pthread_cond_wait ()
#6  0xaec06318 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 7 (LWP 13925):
#0  0xb5c00ab4 in epoll_wait (epfd=34, events=0xafa007c8, maxevents=32, timeout=-1) at ../sysdeps/unix/sysv/linux/epoll_wait.c:30
#1  0x0050fd84 in epoll_dispatch ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 6 (LWP 13923):
#0  0xb5b8d6f8 in __futex_abstimed_wait_common32 (private=<optimized out>, futex_word=<optimized out>, expected=<optimized out>, op=<optimized out>, abstime=<optimized out>, cancel=<optimized out>) at futex-internal.c:40
#1  __futex_abstimed_wait_common (futex_word=0x5bf788, futex_word@entry=0x0, expected=expected@entry=0, clockid=clockid@entry=6026948, abstime=abstime@entry=0x0, private=0, private@entry=6027104, cancel=cancel@entry=true) at futex-internal.c:99
#2  0xb5b8d838 in __GI___futex_abstimed_wait_cancelable64 (futex_word=futex_word@entry=0x0, expected=expected@entry=0, clockid=clockid@entry=6026948, abstime=abstime@entry=0x0, private=private@entry=0) at futex-internal.c:139
#3  0xb5b90514 in __pthread_cond_wait_common (cond=0x5bf760, mutex=0x0, clockid=6026948, abstime=<optimized out>) at pthread_cond_wait.c:503
#4  ___pthread_cond_timedwait64 (cond=0x5bf760, mutex=0x0, abstime=<optimized out>) at pthread_cond_wait.c:643
#5  0xb5b90614 in ___pthread_cond_timedwait (cond=<optimized out>, mutex=<optimized out>, abstime=<optimized out>) at pthread_cond_wait.c:658
#6  0x00413ebc in __abi_wrap_pthread_cond_timedwait ()
#7  0xaec063f8 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 5 (LWP 13922):
#0  0xb5b8d6f8 in __futex_abstimed_wait_common32 (private=<optimized out>, futex_word=<optimized out>, expected=<optimized out>, op=<optimized out>, abstime=<optimized out>, cancel=<optimized out>) at futex-internal.c:40
#1  __futex_abstimed_wait_common (futex_word=0xb05fe58c, futex_word@entry=0xaebd8314, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=0, private@entry=-1335892636, cancel=cancel@entry=true) at futex-internal.c:99
#2  0xb5b8d838 in __GI___futex_abstimed_wait_cancelable64 (futex_word=futex_word@entry=0xaebd8314, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=private@entry=0) at futex-internal.c:139
#3  0xb5b901bc in __pthread_cond_wait_common (cond=0xb05fe564, mutex=0xb05fe58c, clockid=0, abstime=0x0) at pthread_cond_wait.c:503
#4  ___pthread_cond_wait (cond=0xb05fe564, mutex=0xb05fe58c) at pthread_cond_wait.c:618
#5  0x004140c8 in __abi_wrap_pthread_cond_wait ()
#6  0xaec06318 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

--Type <RET> for more, q to quit, c to continue without paging--
Thread 4 (LWP 13921):
#0  0xb5b8d6f8 in __futex_abstimed_wait_common32 (private=<optimized out>, futex_word=<optimized out>, expected=<optimized out>, op=<optimized out>, abstime=<optimized out>, cancel=<optimized out>) at futex-internal.c:40
#1  __futex_abstimed_wait_common (futex_word=0xb11d5634, futex_word@entry=0x0, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=0, private@entry=-1323477492, cancel=cancel@entry=true) at futex-internal.c:99
#2  0xb5b8d838 in __GI___futex_abstimed_wait_cancelable64 (futex_word=futex_word@entry=0x0, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=private@entry=0) at futex-internal.c:139
#3  0xb5b901bc in __pthread_cond_wait_common (cond=0xb11d560c, mutex=0xb11d5634, clockid=0, abstime=0x0) at pthread_cond_wait.c:503
#4  ___pthread_cond_wait (cond=0xb11d560c, mutex=0xb11d5634) at pthread_cond_wait.c:618
#5  0x004140c8 in __abi_wrap_pthread_cond_wait ()
#6  0xaec06318 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 3 (LWP 13920):
#0  0xb5b8d6f8 in __futex_abstimed_wait_common32 (private=<optimized out>, futex_word=<optimized out>, expected=<optimized out>, op=<optimized out>, abstime=<optimized out>, cancel=<optimized out>) at futex-internal.c:40
#1  __futex_abstimed_wait_common (futex_word=0xb19d657c, futex_word@entry=0x56b504 <pthread_cond_wait@got.plt>, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=0, private@entry=-1315084972, cancel=cancel@entry=true) at futex-internal.c:99
#2  0xb5b8d838 in __GI___futex_abstimed_wait_cancelable64 (futex_word=futex_word@entry=0x56b504 <pthread_cond_wait@got.plt>, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=private@entry=0) at futex-internal.c:139
#3  0xb5b901bc in __pthread_cond_wait_common (cond=0xb19d6554, mutex=0xb19d657c, clockid=0, abstime=0x0) at pthread_cond_wait.c:503
#4  ___pthread_cond_wait (cond=0xb19d6554, mutex=0xb19d657c) at pthread_cond_wait.c:618
#5  0x004140c8 in __abi_wrap_pthread_cond_wait ()
#6  0xaec06318 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 2 (LWP 13918):
#0  0xb5b8d6f8 in __futex_abstimed_wait_common32 (private=<optimized out>, futex_word=<optimized out>, expected=<optimized out>, op=<optimized out>, abstime=<optimized out>, cancel=<optimized out>) at futex-internal.c:40
#1  __futex_abstimed_wait_common (futex_word=0x5a4230, futex_word@entry=0x0, expected=453385815, expected@entry=0, clockid=clockid@entry=5915108, abstime=abstime@entry=0x0, private=0, private@entry=5915144, cancel=cancel@entry=true) at futex-internal.c:99
#2  0xb5b8d838 in __GI___futex_abstimed_wait_cancelable64 (futex_word=futex_word@entry=0x0, expected=expected@entry=0, clockid=clockid@entry=5915108, abstime=abstime@entry=0x0, private=private@entry=0) at futex-internal.c:139
#3  0xb5b90514 in __pthread_cond_wait_common (cond=0x5a4208, mutex=0x0, clockid=5915108, abstime=<optimized out>) at pthread_cond_wait.c:503
#4  ___pthread_cond_timedwait64 (cond=0x5a4208, mutex=0x0, abstime=<optimized out>) at pthread_cond_wait.c:643
#5  0xb5b90614 in ___pthread_cond_timedwait (cond=<optimized out>, mutex=<optimized out>, abstime=<optimized out>) at pthread_cond_wait.c:658
#6  0x00446df4 in starboard::ConditionVariable::WaitTimed(long long) const ()
#7  0x00446b0c in starboard::Semaphore::TakeWait(long long) ()
#8  0x00446510 in starboard::Thread::WaitForJoin(long long) ()
#9  0x00506a9c in starboard::shared::signal::SignalHandlerThread::Run() ()
#10 0x00445dd0 in starboard::Thread::ThreadEntryPoint(void*) ()
#11 0xb5b90eac in start_thread (arg=0xb21d7e60) at pthread_create.c:447
#12 0xb5c0048c in ?? () at ../sysdeps/unix/sysv/linux/arm/clone3.S:71 from /lib/libc.so.6
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 1 (LWP 13889):
#0  0xb5b8d6f8 in __futex_abstimed_wait_common32 (private=<optimized out>, futex_word=<optimized out>, expected=<optimized out>, op=<optimized out>, abstime=<optimized out>, cancel=<optimized out>) at futex-internal.c:40
#1  __futex_abstimed_wait_common (futex_word=0xbeffde94, futex_word@entry=0xbeffdcd8, expected=25329656, expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=0, private@entry=-1090527636, cancel=cancel@entry=true) at futex-internal.c:99
#2  0xb5b8d838 in __GI___futex_abstimed_wait_cancelable64 (futex_word=futex_word@entry=0xbeffdcd8, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=private@entry=0) at futex-internal.c:139
#3  0xb5b901bc in __pthread_cond_wait_common (cond=0xbeffde6c, mutex=0xbeffde94, clockid=0, abstime=0x0) at pthread_cond_wait.c:503
#4  ___pthread_cond_wait (cond=0xbeffde6c, mutex=0xbeffde94) at pthread_cond_wait.c:618
#5  0x004140c8 in __abi_wrap_pthread_cond_wait ()
#6  0xaec06318 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)
(gdb) mesa-debugsource-24.3.4-0.armv7l
