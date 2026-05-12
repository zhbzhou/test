四、你现在 crash 的本质一句话总结

Mesa 24 在你的 Tizen + HAL GLES + disabled LLVM 环境下，错误选择 softpipe + threaded rasterizer，导致 EGL pipe_screen 初始化不完整，Rasterizer worker thread 访问 NULL context → SIGSEGV。
