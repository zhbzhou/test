Thread 1 "cobalt_launcher" hit Breakpoint 1, __pthread_create_2_1 (newthread=0x5ddca0, attr=0xbeffdac0, start_routine=0xb60d0509, arg=0x5ddc80) at pthread_create.c:632
632     in pthread_create.c
(gdb) bt
#0  __pthread_create_2_1 (newthread=0x5ddca0, attr=0xbeffdac0, start_routine=0xb60d0509, arg=0x5ddc80) at pthread_create.c:632
#1  0xb60f2706 in ?? () from /lib/libglib-2.0.so.0
#2  0xb60d08f4 in g_thread_new () from /lib/libglib-2.0.so.0
#3  0xb07b3a66 in tpl_gthread_create () from /lib/libtpl-egl.so.1
#4  0xb07b8fac in ?? () from /lib/libtpl-egl.so.1
#5  0xb07b0ffc in tpl_display_create () from /lib/libtpl-egl.so.1
#6  0xb1133962 in dri2_initialize_tizen (disp=disp@entry=0x60cc08) at ../src/egl/drivers/dri2/platform_tizen.c:1440
#7  0xb11318c0 in dri2_initialize (disp=0x60cc08) at ../src/egl/drivers/dri2/egl_dri2.c:930
#8  0xb1124322 in eglInitialize (dpy=<optimized out>, major=0x0, minor=0x0) at ../src/egl/main/eglapi.c:722
#9  0xaf2b2a88 in ?? ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)
(gdb) c
Continuing.
[New LWP 4806]

Thread 1 "cobalt_launcher" hit Breakpoint 1, __pthread_create_2_1 (newthread=0xbeffdcac, attr=0xbeffdcb0, start_routine=0xaec086f4, arg=0xbe0408) at pthread_create.c:632
632     in pthread_create.c
(gdb) bt
#0  __pthread_create_2_1 (newthread=0xbeffdcac, attr=0xbeffdcb0, start_routine=0xaec086f4, arg=0xbe0408) at pthread_create.c:632
#1  0x00414518 in __abi_wrap_pthread_create ()
Backtrace stopped: previous frame identical to this frame (corrupt stack?)
(gdb) c
Continuing.
[New LWP 4861]

Thread 20 "Rasterizer" received signal SIGSEGV, Segmentation fault.
[Switching to LWP 4861]
0xaf446f90 in ?? ()
(gdb)
