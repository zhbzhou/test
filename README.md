  406s] + /etc/hal/rootstrap/hal-rootstrap-checker.sh /home/abuild/rpmbuild/SOURCES /home/abuild/rpmbuild/BUILDROOT/mesa-23.3.3-0.arm arm
[  406s] Package:  enabled gallium drivers : kmsro,swrast,vc4,v3d,virgl, Group:  enabled gallium drivers : kmsro,swrast,vc4,v3d,virgl
[  406s] # NOTICE: Config app-rootstrap-checker.yaml skipped                                      #
[  406s] Matched Config: hal-rootstrap-checker.yaml -> Running checks...
[  406s] ##########################################################################################
[  406s] ##########################################################################################
[  406s] # ERROR: There are not allowed BuildRequires. They might cause ABI break.                #
[  406s] # ERROR:  -  enabled gallium drivers : kmsro,swrast,vc4,v3d,virgl, Group: Unspecified    #
[  406s] # ERROR:  - bison, Group: Platform Development/Utilities                                 #
[  406s] # ERROR:  - flex, Group: Development/Languages/C and C++                                 #
[  406s] # ERROR:  - meson, Group: Development/Tools/Building                                     #
[  406s] # ERROR:  - pkgconfig, Group: Unspecified                                                #
[  406s] # ERROR:  - pkgconfig(dlog), Group: System/Libraries                                     #
[  406s] # ERROR:  - pkgconfig(expat), Group: Unspecified                                         #
[  406s] # ERROR:  - pkgconfig(libdrm) >= 2.4.75, Group: Graphics & UI Framework/Libraries        #
[  406s] # ERROR:  - pkgconfig(libsystemd), Group: Base/Startup                                   #
[  406s] # ERROR:  - pkgconfig(libtbm), Group: System/Libraries                                   #
[  406s] # ERROR:  - pkgconfig(libtdm), Group: Development/Libraries                              #
[  406s] # ERROR:  - pkgconfig(libudev) > 150, Group: Unspecified                                 #
[  406s] # ERROR:  - pkgconfig(tpl-egl), Group: Unspecified                                       #
[  406s] # ERROR:  - pkgconfig(ttrace), Group: System/Libraries                                   #
[  406s] # ERROR:  - pkgconfig(wayland-client), Group: Unspecified                                #
[  406s] # ERROR:  - pkgconfig(wayland-protocols), Group: Graphics & UI Framework/Development     #
[  406s] # ERROR:  - pkgconfig(wayland-server), Group: Unspecified                                #
[  406s] # ERROR:  - pkgconfig(zlib), Group: Base/Libraries                                       #
[  406s] # ERROR:  - python3, Group: Development/Languages/Python                                 #
[  406s] # ERROR:  - python3-mako, Group: Development/Languages/Python                            #
[  406s] # ERROR:                                                                                 #
[  406s] # ERROR: Use only allowed packages below for BuildRequires                               #
[  406s] # ERROR:  - cmake                                                                        #
[  406s] # ERROR:  - pkgconfig(hal-rootstrap)                                                     #
[  406s] # ERROR:  - linux-glibc-devel                                                            #
[  406s] # ERROR:  - kernel-headers-*                                                             #
[  406s] ##########################################################################################
[  406s] ##########################################################################################
[  406s] ##########################################################################################
[  406s] ##########################################################################################
[  406s] # ERROR: There are not allowed BuildConflicts. They might cause ABI break.               #
[  406s] # ERROR:  -  enabled gallium drivers : kmsro,swrast,vc4,v3d,virgl, Group: Unspecified    #
[  406s] # ERROR:                                                                                 #
[  406s] # ERROR: Use only allowed packages below for BuildConflicts                              #
[  406s] # ERROR:  - linux-glibc-devel                                                            #
[  406s] # ERROR:  - kernel-headers-*                                                             #
[  406s] ##########################################################################################
[  406s] ##########################################################################################
[  406s] FAILURE: Violation detected.
[  406s] error: Bad exit status from /var/tmp/rpm-tmp.uhQxSX (%install)
[  406s]
[  406s]
[  406s] RPM build errors:
[  406s]     Bad exit status from /var/tmp/rpm-tmp.uhQxSX (%install)
[  406s]
[  406s] zhbzhou failed "build mesa.spec" at Sat May  9 01:28:27 UTC 2026.
[  406s]
warning: build failed, Leaving the logs in /home/zhbzhou/GBS-ROOT-Tizen10/local/repos/tizen/armv7l/logs/fail/mesa-23.3.3-0/log.txt
