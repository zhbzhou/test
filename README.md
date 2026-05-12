Thread 21 "Rasterizer" received signal SIGSEGV, Segmentation fault.
[Switching to LWP 8262]
0xaf446f90 in ?? ()
(gdb) x/20i 0xaf446f90
=> 0xaf446f90:  ldr     r0, [r0, #56]   ; 0x38
   0xaf446f94:  mov     r1, r2
   0xaf446f98:  b       0xaf469064
   0xaf446f9c:  push    {r4, r5, r6, lr}
   0xaf446fa0:  sub     sp, sp, #8
   0xaf446fa4:  ldr     r5, [r0, #80]   ; 0x50
   0xaf446fa8:  mov     r4, r0
   0xaf446fac:  cmp     r5, #0
   0xaf446fb0:  bne     0xaf446ff4
   0xaf446fb4:  mov     r0, #40 ; 0x28
   0xaf446fb8:  bl      0xaf678d70
   0xaf446fbc:  mov     r5, r0
   0xaf446fc0:  bl      0xaf521e68
   0xaf446fc4:  ldr     r0, [r4, #80]   ; 0x50
   0xaf446fc8:  str     r5, [r4, #80]   ; 0x50
   0xaf446fcc:  cmp     r0, #0
   0xaf446fd0:  beq     0xaf446fe0
   0xaf446fd4:  bl      0xaf521ea8
   0xaf446fd8:  bl      0xaf678d90
   0xaf446fdc:  ldr     r5, [r4, #80]   ; 0x50
(gdb)

meson setup --prefix %{_hal_prefix} build/ \
        -Dc_link_args="-lttrace" \
        -Dcpp_link_args="-lttrace" \
        -Dlibdir=%{_hal_libdir} \
        -Dgallium-va=disabled \
        -Dgallium-vdpau=disabled \
        -Dgallium-xa=disabled \
        -Dglx=disabled \
        -Ddraw-use-llvm=false \
        -Dllvm=disabled \
        -Dgbm=%{?enable_gbm:enabled}%{?!enable_gbm:disabled} \
        -Dplatforms="tizen" \
        -Dgallium-drivers=%{gallium_drivers} \
        -Dvulkan-drivers=%{vulkan_drivers}
		
		[   34s] meson.build:1814:2: ERROR: Problem encountered: llvmpipe requires LLVM and is enabled, but LLVM is disabled.
