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
[New LWP 32157]
[32128:32128:19700101,104812.581346:INFO crashpad_client_linux.cc:333] Added evergreen info: --evergreen-information=0x5a8960
[32128:32128:19700101,104812.582748:INFO crashpad_client_linux.cc:96] Added annotation: --annotation=user_agent_string=Mozilla/5.0 (Tizen; /6.0/2025.30.1034943) Cobalt/25.lts.30.1034943-qa (unlike Gecko) v8/8.8.278.17-jit gles Evergreen/5.30.2 Evergreen-Full Evergreen-Compressed Starboard/16, Samsung_TV_PONTUSM_2021/T-NKM2AKUC (Samsung, QAQ80)
[New LWP 32159]
[New LWP 32160]
[New LWP 32161]
[New LWP 32162]
[New LWP 32164]
[New LWP 32163]
[New LWP 32165]
[New LWP 32166]
[New LWP 32167]
[32128:32128:19700101,104812.596099:INFO crashpad_client_linux.cc:85] Updated annotation: --annotation=user_agent_string=Mozilla/5.0 (Tizen; /6.0/2025.30.1034943) Cobalt/25.lts.30.1034943-qa (unlike Gecko) v8/8.8.278.17-jit gles Evergreen/5.30.2 Evergreen-Full Evergreen-Compressed Starboard/16, Samsung_TV_PONTUSM_2021/T-NKM2AKUC (Samsung, QAQ80)
[32128:32128:19700101,104812.596389:INFO crashpad_client_linux.cc:85] Updated annotation: --annotation=prod=Cobalt_Evergreen
[32128:32128:19700101,104812.596444:INFO crashpad_client_linux.cc:85] Updated annotation: --annotation=ver=5.30.2
[New LWP 32168]
[New LWP 32169]
[New LWP 32170]
[New LWP 32171]
[New LWP 32172]
[New LWP 32173]
[New LWP 32174]
[New LWP 32189]
[New LWP 32190]
[New LWP 32191]

Thread 21 "Rasterizer" received signal SIGSEGV, Segmentation fault.
[Switching to LWP 32191]
0xaf446f90 in ?? ()
(gdb) thread apply all bt

Thread 21 (LWP 32191):
#0  0xaf446f90 in ?? ()
#1  0xaf655b10 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 20 (LWP 32190):
#0  0xb5b8d6f8 in __futex_abstimed_wait_common32 (private=<optimized out>, futex_word=<optimized out>, expected=<optimized out>, op=<optimized out>, abstime=<optimized out>, cancel=<optimized out>) at futex-internal.c:40
#1  __futex_abstimed_wait_common (futex_word=0x5f60d8, futex_word@entry=0xa72c5344 <pthread_cond_wait@got.plt>, expected=2782767012, expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=0, private@entry=6250672, cancel=cancel@entry=true) at futex-internal.c:99
#2  0xb5b8d838 in __GI___futex_abstimed_wait_cancelable64 (futex_word=futex_word@entry=0xa72c5344 <pthread_cond_wait@got.plt>, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=private@entry=0) at futex-internal.c:139
#3  0xb5b901bc in __pthread_cond_wait_common (cond=0x5f60b0, mutex=0x5f60d8, clockid=0, abstime=0x0) at pthread_cond_wait.c:503
#4  ___pthread_cond_wait (cond=0x5f60b0, mutex=0x5f60d8) at pthread_cond_wait.c:618
#5  0xa6aa321a in cnd_wait (cond=<optimized out>, mtx=<optimized out>) at ../src/c11/impl/threads_posix.c:111
#6  0xa6a8a148 in util_queue_thread_func (input=<optimized out>) at ../src/util/u_queue.c:275
#7  0xb5b90eac in start_thread (arg=0xa5ddae60) at pthread_create.c:447
#8  0xb5c0048c in ?? () at ../sysdeps/unix/sysv/linux/arm/clone3.S:71 from /lib/libc.so.6
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 19 (LWP 32189):
#0  0xb5bf5a18 in __GI___poll (fds=0x615208, nfds=7, timeout=-1) at ../sysdeps/unix/sysv/linux/poll.c:29
#1  __GI___poll (fds=0x615208, nfds=7, timeout=-1) at ../sysdeps/unix/sysv/linux/poll.c:26
#2  0xb60b1278 in ?? () from /lib/libglib-2.0.so.0
#3  0xb60b182e in g_main_loop_run () from /lib/libglib-2.0.so.0
#4  0xb07b36e6 in ?? () from /lib/libtpl-egl.so.1
#5  0xb60d0532 in ?? () from /lib/libglib-2.0.so.0
#6  0xb5b90eac in start_thread (arg=0xa671ce60) at pthread_create.c:447
#7  0xb5c0048c in ?? () at ../sysdeps/unix/sysv/linux/arm/clone3.S:71 from /lib/libc.so.6
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 18 (LWP 32174):
#0  0xb5bf5a18 in __GI___poll (fds=0x60ffb8, nfds=2, timeout=-1) at ../sysdeps/unix/sysv/linux/poll.c:29
#1  __GI___poll (fds=0x60ffb8, nfds=2, timeout=-1) at ../sysdeps/unix/sysv/linux/poll.c:26
#2  0xb60b1278 in ?? () from /lib/libglib-2.0.so.0
#3  0xb60b182e in g_main_loop_run () from /lib/libglib-2.0.so.0
#4  0xb5aab20a in ?? () from /lib/libgio-2.0.so.0
#5  0xb60d0532 in ?? () from /lib/libglib-2.0.so.0
#6  0xb5b90eac in start_thread (arg=0xa7af7e60) at pthread_create.c:447
#7  0xb5c0048c in ?? () at ../sysdeps/unix/sysv/linux/arm/clone3.S:71 from /lib/libc.so.6
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 17 (LWP 32173):
#0  0xb5bf5a18 in __GI___poll (fds=0xb0600c70, nfds=1, timeout=-1) at ../sysdeps/unix/sysv/linux/poll.c:29
#1  __GI___poll (fds=0xb0600c70, nfds=1, timeout=-1) at ../sysdeps/unix/sysv/linux/poll.c:26
#2  0xb60b1278 in ?? () from /lib/libglib-2.0.so.0
#3  0xb60b164c in g_main_context_iteration () from /lib/libglib-2.0.so.0
#4  0xb60b1674 in ?? () from /lib/libglib-2.0.so.0
#5  0xb60d0532 in ?? () from /lib/libglib-2.0.so.0
#6  0xb5b90eac in start_thread (arg=0xa82f8e60) at pthread_create.c:447
#7  0xb5c0048c in ?? () at ../sysdeps/unix/sysv/linux/arm/clone3.S:71 from /lib/libc.so.6
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 16 (LWP 32172):
#0  syscall () at ../sysdeps/unix/sysv/linux/arm/syscall.S:37
#1  0xb60f29d4 in g_cond_wait () from /lib/libglib-2.0.so.0
#2  0xb6089626 in ?? () from /lib/libglib-2.0.so.0
#3  0xb60d0b20 in ?? () from /lib/libglib-2.0.so.0
#4  0xb60d0532 in ?? () from /lib/libglib-2.0.so.0
#5  0xb5b90eac in start_thread (arg=0xa8af9e60) at pthread_create.c:447
#6  0xb5c0048c in ?? () at ../sysdeps/unix/sysv/linux/arm/clone3.S:71 from /lib/libc.so.6
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 15 (LWP 32171):
#0  0xb5b8d6f8 in __futex_abstimed_wait_common32 (private=<optimized out>, futex_word=<optimized out>, expected=<optimized out>, op=<optimized out>, abstime=<optimized out>, cancel=<optimized out>) at futex-internal.c:40
#1  __futex_abstimed_wait_common (futex_word=0xa92fa58c, futex_word@entry=0xaebd8314, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=0, private@entry=-1456495260, cancel=cancel@entry=true) at futex-internal.c:99
#2  0xb5b8d838 in __GI___futex_abstimed_wait_cancelable64 (futex_word=futex_word@entry=0xaebd8314, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=private@entry=0) at futex-internal.c:139
#3  0xb5b901bc in __pthread_cond_wait_common (cond=0xa92fa564, mutex=0xa92fa58c, clockid=0, abstime=0x0) at pthread_cond_wait.c:503
#4  ___pthread_cond_wait (cond=0xa92fa564, mutex=0xa92fa58c) at pthread_cond_wait.c:618
#5  0x004140c8 in __abi_wrap_pthread_cond_wait ()
#6  0xaec06318 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 14 (LWP 32170):
#0  0xb5b8d6f8 in __futex_abstimed_wait_common32 (private=<optimized out>, futex_word=<optimized out>, expected=<optimized out>, op=<optimized out>, abstime=<optimized out>, cancel=<optimized out>) at futex-internal.c:40
#1  __futex_abstimed_wait_common (futex_word=0xa9afb58c, futex_word@entry=0x0, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=0, private@entry=-1448102556, cancel=cancel@entry=true) at futex-internal.c:99
#2  0xb5b8d838 in __GI___futex_abstimed_wait_cancelable64 (futex_word=futex_word@entry=0x0, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=private@entry=0) at futex-internal.c:139
#3  0xb5b901bc in __pthread_cond_wait_common (cond=0xa9afb564, mutex=0xa9afb58c, clockid=0, abstime=0x0) at pthread_cond_wait.c:503
#4  ___pthread_cond_wait (cond=0xa9afb564, mutex=0xa9afb58c) at pthread_cond_wait.c:618
#5  0x004140c8 in __abi_wrap_pthread_cond_wait ()
#6  0xaec06318 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

--Type <RET> for more, q to quit, c to continue without paging--
Thread 13 (LWP 32169):
#0  0xb5b8d6f8 in __futex_abstimed_wait_common32 (private=<optimized out>, futex_word=<optimized out>, expected=<optimized out>, op=<optimized out>, abstime=<optimized out>, cancel=<optimized out>) at futex-internal.c:40
#1  __futex_abstimed_wait_common (futex_word=0xaa2fc594, futex_word@entry=0xaa2fc380, expected=expected@entry=0, clockid=clockid@entry=-1439709928, abstime=abstime@entry=0x0, private=0, private@entry=-1439709844, cancel=cancel@entry=true) at futex-internal.c:99
#2  0xb5b8d838 in __GI___futex_abstimed_wait_cancelable64 (futex_word=futex_word@entry=0xaa2fc380, expected=expected@entry=0, clockid=clockid@entry=-1439709928, abstime=abstime@entry=0x0, private=0, private@entry=81) at futex-internal.c:139
#3  0xb5b90514 in __pthread_cond_wait_common (cond=0xaa2fc56c, mutex=0x0, clockid=-1439709928, abstime=<optimized out>) at pthread_cond_wait.c:503
#4  ___pthread_cond_timedwait64 (cond=0xaa2fc56c, mutex=0x0, abstime=<optimized out>) at pthread_cond_wait.c:643
#5  0xb5b90614 in ___pthread_cond_timedwait (cond=<optimized out>, mutex=<optimized out>, abstime=<optimized out>) at pthread_cond_wait.c:658
#6  0x00413ebc in __abi_wrap_pthread_cond_timedwait ()
#7  0xaec063f8 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 12 (LWP 32168):
#0  0xb5c00ab4 in epoll_wait (epfd=39, events=0xab303248, maxevents=32, timeout=30000) at ../sysdeps/unix/sysv/linux/epoll_wait.c:30
#1  0x0050fd84 in epoll_dispatch ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 11 (LWP 32167):
#0  0xb5b8d6f8 in __futex_abstimed_wait_common32 (private=<optimized out>, futex_word=<optimized out>, expected=<optimized out>, op=<optimized out>, abstime=<optimized out>, cancel=<optimized out>) at futex-internal.c:40
#1  __futex_abstimed_wait_common (futex_word=0xab2fe58c, futex_word@entry=0xaebd8314, expected=33152, expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=0, private@entry=-1422924444, cancel=cancel@entry=true) at futex-internal.c:99
#2  0xb5b8d838 in __GI___futex_abstimed_wait_cancelable64 (futex_word=futex_word@entry=0xaebd8314, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=private@entry=0) at futex-internal.c:139
#3  0xb5b901bc in __pthread_cond_wait_common (cond=0xab2fe564, mutex=0xab2fe58c, clockid=0, abstime=0x0) at pthread_cond_wait.c:503
#4  ___pthread_cond_wait (cond=0xab2fe564, mutex=0xab2fe58c) at pthread_cond_wait.c:618
#5  0x004140c8 in __abi_wrap_pthread_cond_wait ()
#6  0xaec06318 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 10 (LWP 32166):
#0  0xb5b8d6f8 in __futex_abstimed_wait_common32 (private=<optimized out>, futex_word=<optimized out>, expected=<optimized out>, op=<optimized out>, abstime=<optimized out>, cancel=<optimized out>) at futex-internal.c:40
#1  __futex_abstimed_wait_common (futex_word=0xabcd858c, futex_word@entry=0xaebd8314, expected=43, expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=0, private@entry=-1412594332, cancel=cancel@entry=true) at futex-internal.c:99
#2  0xb5b8d838 in __GI___futex_abstimed_wait_cancelable64 (futex_word=futex_word@entry=0xaebd8314, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=private@entry=0) at futex-internal.c:139
#3  0xb5b901bc in __pthread_cond_wait_common (cond=0xabcd8564, mutex=0xabcd858c, clockid=0, abstime=0x0) at pthread_cond_wait.c:503
#4  ___pthread_cond_wait (cond=0xabcd8564, mutex=0xabcd858c) at pthread_cond_wait.c:618
#5  0x004140c8 in __abi_wrap_pthread_cond_wait ()
#6  0xaec06318 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 9 (LWP 32165):
#0  0xb5b8d6f8 in __futex_abstimed_wait_common32 (private=<optimized out>, futex_word=<optimized out>, expected=<optimized out>, op=<optimized out>, abstime=<optimized out>, cancel=<optimized out>) at futex-internal.c:40
#1  __futex_abstimed_wait_common (futex_word=0xac4d958c, futex_word@entry=0xaebd8314, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=0, private@entry=-1404201628, cancel=cancel@entry=true) at futex-internal.c:99
#2  0xb5b8d838 in __GI___futex_abstimed_wait_cancelable64 (futex_word=futex_word@entry=0xaebd8314, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=private@entry=0) at futex-internal.c:139
#3  0xb5b901bc in __pthread_cond_wait_common (cond=0xac4d9564, mutex=0xac4d958c, clockid=0, abstime=0x0) at pthread_cond_wait.c:503
#4  ___pthread_cond_wait (cond=0xac4d9564, mutex=0xac4d958c) at pthread_cond_wait.c:618
#5  0x004140c8 in __abi_wrap_pthread_cond_wait ()
#6  0xaec06318 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 8 (LWP 32163):
#0  0xb5b8d6f8 in __futex_abstimed_wait_common32 (private=<optimized out>, futex_word=<optimized out>, expected=<optimized out>, op=<optimized out>, abstime=<optimized out>, cancel=<optimized out>) at futex-internal.c:40
#1  __futex_abstimed_wait_common (futex_word=0xaccda634, futex_word@entry=0x0, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=0, private@entry=-1395808756, cancel=cancel@entry=true) at futex-internal.c:99
#2  0xb5b8d838 in __GI___futex_abstimed_wait_cancelable64 (futex_word=futex_word@entry=0x0, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=private@entry=0) at futex-internal.c:139
#3  0xb5b901bc in __pthread_cond_wait_common (cond=0xaccda60c, mutex=0xaccda634, clockid=0, abstime=0x0) at pthread_cond_wait.c:503
#4  ___pthread_cond_wait (cond=0xaccda60c, mutex=0xaccda634) at pthread_cond_wait.c:618
#5  0x004140c8 in __abi_wrap_pthread_cond_wait ()
#6  0xaec06318 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 7 (LWP 32164):
#0  0xb5c00ab4 in epoll_wait (epfd=34, events=0xaf8007c8, maxevents=32, timeout=-1) at ../sysdeps/unix/sysv/linux/epoll_wait.c:30
#1  0x0050fd84 in epoll_dispatch ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 6 (LWP 32162):
#0  0xb5b8d6f8 in __futex_abstimed_wait_common32 (private=<optimized out>, futex_word=<optimized out>, expected=<optimized out>, op=<optimized out>, abstime=<optimized out>, cancel=<optimized out>) at futex-internal.c:40
#1  __futex_abstimed_wait_common (futex_word=0x5bf6b8, futex_word@entry=0x0, expected=expected@entry=0, clockid=clockid@entry=6026740, abstime=abstime@entry=0x0, private=0, private@entry=6026896, cancel=cancel@entry=true) at futex-internal.c:99
#2  0xb5b8d838 in __GI___futex_abstimed_wait_cancelable64 (futex_word=futex_word@entry=0x0, expected=expected@entry=0, clockid=clockid@entry=6026740, abstime=abstime@entry=0x0, private=private@entry=0) at futex-internal.c:139
#3  0xb5b90514 in __pthread_cond_wait_common (cond=0x5bf690, mutex=0x0, clockid=6026740, abstime=<optimized out>) at pthread_cond_wait.c:503
#4  ___pthread_cond_timedwait64 (cond=0x5bf690, mutex=0x0, abstime=<optimized out>) at pthread_cond_wait.c:643
#5  0xb5b90614 in ___pthread_cond_timedwait (cond=<optimized out>, mutex=<optimized out>, abstime=<optimized out>) at pthread_cond_wait.c:658
#6  0x00413ebc in __abi_wrap_pthread_cond_timedwait ()
#7  0xaec063f8 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 5 (LWP 32161):
#0  0xb5b8d6f8 in __futex_abstimed_wait_common32 (private=<optimized out>, futex_word=<optimized out>, expected=<optimized out>, op=<optimized out>, abstime=<optimized out>, cancel=<optimized out>) at futex-internal.c:40
#1  __futex_abstimed_wait_common (futex_word=0xb05fe58c, futex_word@entry=0xaebd8314, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=0, private@entry=-1335892636, cancel=cancel@entry=true) at futex-internal.c:99
#2  0xb5b8d838 in __GI___futex_abstimed_wait_cancelable64 (futex_word=futex_word@entry=0xaebd8314, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=private@entry=0) at futex-internal.c:139
#3  0xb5b901bc in __pthread_cond_wait_common (cond=0xb05fe564, mutex=0xb05fe58c, clockid=0, abstime=0x0) at pthread_cond_wait.c:503
#4  ___pthread_cond_wait (cond=0xb05fe564, mutex=0xb05fe58c) at pthread_cond_wait.c:618
#5  0x004140c8 in __abi_wrap_pthread_cond_wait ()
#6  0xaec06318 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

--Type <RET> for more, q to quit, c to continue without paging--
Thread 4 (LWP 32160):
#0  0xb5b8d6f8 in __futex_abstimed_wait_common32 (private=<optimized out>, futex_word=<optimized out>, expected=<optimized out>, op=<optimized out>, abstime=<optimized out>, cancel=<optimized out>) at futex-internal.c:40
#1  __futex_abstimed_wait_common (futex_word=0xb0ffe634, futex_word@entry=0x0, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=0, private@entry=-1325406708, cancel=cancel@entry=true) at futex-internal.c:99
#2  0xb5b8d838 in __GI___futex_abstimed_wait_cancelable64 (futex_word=futex_word@entry=0x0, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=private@entry=0) at futex-internal.c:139
#3  0xb5b901bc in __pthread_cond_wait_common (cond=0xb0ffe60c, mutex=0xb0ffe634, clockid=0, abstime=0x0) at pthread_cond_wait.c:503
#4  ___pthread_cond_wait (cond=0xb0ffe60c, mutex=0xb0ffe634) at pthread_cond_wait.c:618
#5  0x004140c8 in __abi_wrap_pthread_cond_wait ()
#6  0xaec06318 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 3 (LWP 32159):
#0  0xb5b8d6f8 in __futex_abstimed_wait_common32 (private=<optimized out>, futex_word=<optimized out>, expected=<optimized out>, op=<optimized out>, abstime=<optimized out>, cancel=<optimized out>) at futex-internal.c:40
#1  __futex_abstimed_wait_common (futex_word=0xb19d657c, futex_word@entry=0x56b504 <pthread_cond_wait@got.plt>, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=0, private@entry=-1315084972, cancel=cancel@entry=true) at futex-internal.c:99
#2  0xb5b8d838 in __GI___futex_abstimed_wait_cancelable64 (futex_word=futex_word@entry=0x56b504 <pthread_cond_wait@got.plt>, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=private@entry=0) at futex-internal.c:139
#3  0xb5b901bc in __pthread_cond_wait_common (cond=0xb19d6554, mutex=0xb19d657c, clockid=0, abstime=0x0) at pthread_cond_wait.c:503
#4  ___pthread_cond_wait (cond=0xb19d6554, mutex=0xb19d657c) at pthread_cond_wait.c:618
#5  0x004140c8 in __abi_wrap_pthread_cond_wait ()
#6  0xaec06318 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)

Thread 2 (LWP 32157):
#0  0xb5b8d6f8 in __futex_abstimed_wait_common32 (private=<optimized out>, futex_word=<optimized out>, expected=<optimized out>, op=<optimized out>, abstime=<optimized out>, cancel=<optimized out>) at futex-internal.c:40
#1  __futex_abstimed_wait_common (futex_word=0x5a4230, futex_word@entry=0x0, expected=143541556, expected@entry=0, clockid=clockid@entry=5915108, abstime=abstime@entry=0x0, private=0, private@entry=5915144, cancel=cancel@entry=true) at futex-internal.c:99
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

Thread 1 (LWP 32128):
#0  0xb5b8d6f8 in __futex_abstimed_wait_common32 (private=<optimized out>, futex_word=<optimized out>, expected=<optimized out>, op=<optimized out>, abstime=<optimized out>, cancel=<optimized out>) at futex-internal.c:40
#1  __futex_abstimed_wait_common (futex_word=0xbeffde94, futex_word@entry=0xbeffdcd8, expected=25264360, expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=0, private@entry=-1090527636, cancel=cancel@entry=true) at futex-internal.c:99
#2  0xb5b8d838 in __GI___futex_abstimed_wait_cancelable64 (futex_word=futex_word@entry=0xbeffdcd8, expected=expected@entry=0, clockid=clockid@entry=0, abstime=abstime@entry=0x0, private=private@entry=0) at futex-internal.c:139
#3  0xb5b901bc in __pthread_cond_wait_common (cond=0xbeffde6c, mutex=0xbeffde94, clockid=0, abstime=0x0) at pthread_cond_wait.c:503
#4  ___pthread_cond_wait (cond=0xbeffde6c, mutex=0xbeffde94) at pthread_cond_wait.c:618
#5  0x004140c8 in __abi_wrap_pthread_cond_wait ()
#6  0xaec06318 in ?? ()
