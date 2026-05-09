root:/tmp> pid=$(pgrep cobalt); if [ -n "$pid" ]; then cat /proc/$pid/maps | grep libGLESv2; else echo "Cobalt not running"; fi
afd30000-afd37000 r-xp 00000000 b3:0a 286        /hal/lib/driver/libGLESv2.so.2.0.0
afd37000-afd46000 ---p 00007000 b3:0a 286        /hal/lib/driver/libGLESv2.so.2.0.0
afd46000-afd47000 r--p 00006000 b3:0a 286        /hal/lib/driver/libGLESv2.so.2.0.0
afd47000-afd48000 rw-p 00007000 b3:0a 286        /hal/lib/driver/libGLESv2.so.2.0.0
b639e000-b63db000 r-xp 00000000 b3:02 389        /usr/lib/libGLESv2.so.2.0
b63db000-b63dc000 r--p 0003c000 b3:02 389        /usr/lib/libGLESv2.so.2.0
b63dc000-b63dd000 rw-p 0003d000 b3:02 389        /usr/lib/libGLESv2.so.2.0


你现在的问题本质是：

只升级了部分 Mesa 组件

导致：

frontend (libEGL/libGLESv2)

和：

backend (gallium)

不是同一 ABI。

正确升级 Mesa 的原则

Mesa 必须：

整套替换

包括：

libEGL.so
libGLESv2.so
libglapi.so
gallium
DRI drivers
GBM

全部来自：

同一次 Mesa24 build
你现在系统里的 Mesa 相关库

从你的 info sharedlibrary：

关键是：

/lib/libEGL.so.1
/lib/libGLESv2.so.2
/hal/lib/driver/libEGL.so
/hal/lib/driver/libGLESv2.so
/hal/lib/libgallium-24.3.4.so
/hal/lib/libglapi.so.0

这些必须统一版本。

Tizen 上最安全的方法
不要覆盖系统库

而是：

建一个 Mesa24 runtime 目录

例如：

/opt/mesa24/

里面放：

/opt/mesa24/lib/libEGL.so
/opt/mesa24/lib/libGLESv2.so
/opt/mesa24/lib/libglapi.so
/opt/mesa24/lib/libgallium.so
第一步：编译 Mesa24

建议：

meson setup build \
  -Dplatforms=wayland \
  -Dgallium-drivers=swrast \
  -Dvulkan-drivers="" \
  -Degl=enabled \
  -Dgles2=enabled \
  -Dshared-glapi=enabled \
  --prefix=/opt/mesa24

然后：

ninja -C build
ninja -C build install
第二步：确认 Mesa24 库完整

应该有：

ls /opt/mesa24/lib

至少：

libEGL.so
libGLESv2.so
libglapi.so
libgallium*.so
第三步：用 LD_LIBRARY_PATH 强制全套 Mesa24

启动前：

export LD_LIBRARY_PATH=/opt/mesa24/lib:$LD_LIBRARY_PATH

非常关键。

这样：

libEGL/libGLESv2/libglapi/gallium

会一起加载。

第四步：验证实际加载的库

运行：

LD_DEBUG=libs ./cobalt_launcher

检查：

libEGL.so
libGLESv2.so

是不是来自：

/opt/mesa24/lib

而不是：

/lib/
第五步：确认 gallium 也是同版本

必须看到：

libgallium-24.x.so

来自：

/opt/mesa24/lib
第六步：避免 Tizen HAL 混入旧库

Tizen 很危险的一点：

/hal/lib/driver/libEGL.so

可能内部：

dlopen("libgallium.so")

或者直接链接旧 glapi。

所以：

你必须让：
readelf -d /hal/lib/driver/libEGL.so

看到：

NEEDED -> libglapi.so

也是 Mesa24。

最容易成功的方法

其实是：

整个 /hal/lib/driver/

全部替换成 Mesa24 build。

包括：

libEGL.so
libGLESv2.so
libglapi.so

而不是只换 gallium。

但注意：

Tizen/Samsung 有 vendor HAL wrapper。

这些：

libtpl-egl.so
libhal-backend-tbm.so

可能：

假设 Mesa23 ABI
调 Mesa internals

所以：

即使全 Mesa24

仍然可能 crash

真正正确做法（工业界）

必须一起 rebuild：

Mesa24
HAL wrapper
TBM backend
Cobalt
你现在先做这个

执行：

LD_DEBUG=libs ./cobalt_launcher 2>&1 | grep -E "EGL|GLES|gallium|glapi"

看：

到底哪些库来自哪里

这一步最关键。

还有一个现实问题

你的：

Cobalt 25.lts

是 Chromium M80 时代。

Mesa24 是 2025 的。

跨度太大。

所以：

即使 ABI 统一

也可能有 runtime incompatibility

尤其：

EGL sync
dma-buf modifiers
threaded GL
Skia GLES assumptions
所以最稳方案依然是
Mesa 23.3.3

因为：

Samsung Evergreen stack

明显是按 Mesa23 验证的。

非要更新到mesa 24版本 给出详细的步骤

你现在的情况是：

Cobalt 原来运行在旧 GPU stack（Mesa 23.x + Samsung HAL）
你强行替换成了 Mesa 24.3.4
/hal/lib/libgallium-24.3.4.so 已经加载
但 libGLESv2.so 仍然链接到 /lib/libGLESv2.so
最终 Rasterizer 线程 SIGSEGV

这已经不是单独替换一个 .so 能解决的问题了。

Mesa 24 需要：

EGL
GLES
gbm
drm
glapi
dri driver
loader
LLVM（如果开启）
Samsung tbm/wayland bridge

全部 ABI 一致。

你现在是“混合栈”：

Mesa24 gallium
+
系统旧 libEGL/libGLES
+
旧 HAL
+
旧 loader

这一定会崩。

你必须整套替换。

一、正确目标结构

你最终要变成：

/hal/lib/libEGL.so                -> Mesa24
/hal/lib/libGLESv2.so             -> Mesa24
/hal/lib/libglapi.so              -> Mesa24
/hal/lib/libgallium-24.3.4.so     -> Mesa24
/usr/lib/dri/*.so                 -> Mesa24

并且：

LD_LIBRARY_PATH=/hal/lib
LIBGL_DRIVERS_PATH=/usr/lib/dri

而不是：

/lib/libEGL.so
/lib/libGLESv2.so
二、最关键的问题

你的系统：

/lib/libGLESv2.so

是三星原厂 GLES wrapper。

它：

不是 Mesa 24 编译的
ABI 不兼容 Mesa24 gallium
调 Mesa24 时参数布局变了
导致 Rasterizer stack corruption

这就是：

Backtrace stopped: corrupt stack

的根本原因。

三、正确做法（完整替换）
STEP 1 编译 Mesa 24

必须启用：

-Degl=enabled
-Dgles2=enabled
-Dshared-glapi=enabled
-Dgbm=enabled
-Dplatforms=wayland
-Dgallium-drivers=swrast
-Ddri-drivers=

例如：

meson setup build \
  --prefix=/opt/mesa24 \
  -Degl=enabled \
  -Dgles2=enabled \
  -Dshared-glapi=enabled \
  -Dgbm=enabled \
  -Dplatforms=wayland \
  -Dgallium-drivers=swrast \
  -Ddri-drivers=

然后：

ninja -C build
ninja -C build install
STEP 2 拷贝完整 runtime

不要只拷一个 gallium。

要整个：

cp /opt/mesa24/lib/libEGL.so* /hal/lib/
cp /opt/mesa24/lib/libGLESv2.so* /hal/lib/
cp /opt/mesa24/lib/libglapi.so* /hal/lib/
cp /opt/mesa24/lib/libgbm.so* /hal/lib/

mkdir -p /usr/lib/dri
cp /opt/mesa24/lib/dri/* /usr/lib/dri/
STEP 3 修正 symlink

现在你系统：

libGLESv2.so -> /lib/libGLESv2.so

这是错误的。

必须改：

cd /hal/lib

rm libGLESv2.so
ln -s libGLESv2.so.2 libGLESv2.so

rm libEGL.so
ln -s libEGL.so.1 libEGL.so

检查：

readlink -f libGLESv2.so

必须输出：

/hal/lib/libGLESv2.so.2

不能是：

/lib/libGLESv2.so
STEP 4 强制 Cobalt 使用 Mesa24

启动前：

export LD_LIBRARY_PATH=/hal/lib
export LIBGL_DRIVERS_PATH=/usr/lib/dri
export EGL_DRIVER=/hal/lib/libEGL.so

然后：

LD_DEBUG=libs ./cobalt_launcher

检查：

必须看到：

loading /hal/lib/libEGL.so
loading /hal/lib/libGLESv2.so
loading /hal/lib/libgallium-24.3.4.so

不能看到：

/lib/libGLESv2.so
/lib/libEGL.so
STEP 5 检查 dri driver

Mesa24 还会加载：

/usr/lib/dri/swrast_dri.so

或者：

kms_swrast_dri.so

没有它也会 crash。

检查：

ls /usr/lib/dri
STEP 6 禁止旧 Samsung GLES

非常关键。

有些 Tizen loader 会 preload：

/lib/libGLESv2.so

你必须：

方法1（推荐）

重命名：

mv /lib/libGLESv2.so /lib/libGLESv2.so.bak
mv /lib/libEGL.so /lib/libEGL.so.bak

然后：

ln -s /hal/lib/libGLESv2.so /lib/libGLESv2.so
ln -s /hal/lib/libEGL.so /lib/libEGL.so
STEP 7 检查 ABI

最重要：

readelf -Ws /hal/lib/libGLESv2.so | grep glBindTexture

以及：

readelf -Ws /lib/libGLESv2.so

如果符号版本不一致：

GLIBCXX
GLAPI
EGL

一定 crash。

四、你现在为什么 crash

你现在：

Cobalt
 -> /lib/libGLESv2.so (旧)
     -> Mesa24 gallium

相当于：

旧 frontend
+
新 backend

Mesa 24 修改了：

dispatch table
context struct
glapi layout
TLS layout

所以：

函数参数错位
栈破坏
SIGSEGV

这是标准 ABI mismatch。

五、为什么 Mesa 23 正常

Mesa 23：

struct gl_context

布局还和三星 wrapper 兼容。

Mesa24：

glthread 改了
dispatch 改了
loader 改了
glapi 改了

三星 wrapper 没同步。

所以：

23 OK
24 crash
六、最稳方案（推荐）

其实最稳的是：

不替换系统 EGL/GLES

而是：

只替换 dri driver

或者：

使用 llvmpipe standalone

否则 Tizen 整个 graphics stack 都可能炸。

七、你现在下一步

你现在最应该执行：

ldd /usr/apps/com.samsung.tv.cobalt/bin/cobalt_launcher | grep GLES

以及：

readlink -f /hal/lib/libGLESv2.so
readlink -f /lib/libGLESv2.so

如果你愿意，我还能继续帮你：

给你 Mesa24 最小稳定配置
给你 Tizen 专用 meson 配置
给你“只替换软件 rasterizer”的安全方案
给你如何避免三星 HAL 崩溃
给你如何让 Cobalt 兼容 Mesa24 的 patch
教你定位 0xaf446f90 属于哪个 Mesa 符号
教你生成带符号 Mesa 调试版
好的

下面给你一套 Tizen/Cobalt → Mesa 24.3.4 完整稳定迁移方案。
目标：

Cobalt
  ↓
Mesa24 EGL/GLES
  ↓
Mesa24 Gallium
  ↓
llvmpipe / swrast

避免：

Samsung GLES wrapper
+
Mesa24 backend

这种 ABI 混搭。

一、推荐最终结构

最终你应该有：

/hal/lib/
    libEGL.so
    libEGL.so.1
    libGLESv2.so
    libGLESv2.so.2
    libglapi.so.0
    libgbm.so.1
    libgallium-24.3.4.so

/usr/lib/dri/
    swrast_dri.so
    kms_swrast_dri.so

并且：

LD_LIBRARY_PATH=/hal/lib
LIBGL_DRIVERS_PATH=/usr/lib/dri
二、编译 Mesa 24（最重要）

不要直接用 PC Linux 默认配置。

Tizen 上必须尽量精简。

1. 下载 Mesa

使用：

Mesa 官方下载

例如：

wget https://archive.mesa3d.org/mesa-24.3.4.tar.xz
tar xf mesa-24.3.4.tar.xz
cd mesa-24.3.4
2. 安装依赖

需要：

meson
ninja
python3
pkg-config
libdrm
wayland
expat
zlib
3. 最关键 Meson 配置

这是 Tizen/Cobalt 最稳配置：

meson setup build \
  --prefix=/opt/mesa24 \
  -Dbuildtype=release \
  -Degl=enabled \
  -Dgles1=disabled \
  -Dgles2=enabled \
  -Dopengl=false \
  -Dgbm=enabled \
  -Dshared-glapi=enabled \
  -Dglx=disabled \
  -Dllvm=disabled \
  -Dosmesa=false \
  -Dplatforms=wayland \
  -Dgallium-drivers=swrast \
  -Dvulkan-drivers= \
  -Ddri-drivers= \
  -Dxmlconfig=disabled
三、为什么这样配置

因为：

禁止：
OpenGL desktop
GLX
Vulkan
LLVM

避免：

ABI 更复杂
额外符号
loader 冲突
Samsung HAL 崩溃
四、编译
ninja -C build
ninja -C build install

最终：

/opt/mesa24/lib

会生成：

libEGL.so
libGLESv2.so
libglapi.so
libgbm.so
libgallium-24.3.4.so
dri/swrast_dri.so
五、替换系统库（关键）
1. 备份旧库
mkdir /backup_gles

cp /lib/libEGL.so* /backup_gles/
cp /lib/libGLESv2.so* /backup_gles/
2. 拷贝 Mesa24
cp /opt/mesa24/lib/libEGL.so* /hal/lib/
cp /opt/mesa24/lib/libGLESv2.so* /hal/lib/
cp /opt/mesa24/lib/libglapi.so* /hal/lib/
cp /opt/mesa24/lib/libgbm.so* /hal/lib/
cp /opt/mesa24/lib/libgallium-24.3.4.so /hal/lib/
3. 拷贝 DRI
mkdir -p /usr/lib/dri

cp /opt/mesa24/lib/dri/* /usr/lib/dri/
六、修正符号链接（非常关键）

进入：

cd /hal/lib

执行：

rm -f libEGL.so
ln -s libEGL.so.1 libEGL.so

rm -f libGLESv2.so
ln -s libGLESv2.so.2 libGLESv2.so

检查：

readlink -f libGLESv2.so

必须输出：

/hal/lib/libGLESv2.so.2

不是：

/lib/libGLESv2.so
七、最关键：替换系统 frontend

你现在 crash 的根本原因：

/lib/libGLESv2.so

仍然是三星旧 wrapper。

必须替换。

方法（推荐）
mv /lib/libEGL.so /lib/libEGL.so.bak
mv /lib/libGLESv2.so /lib/libGLESv2.so.bak

然后：

ln -s /hal/lib/libEGL.so /lib/libEGL.so
ln -s /hal/lib/libGLESv2.so /lib/libGLESv2.so
八、验证加载路径

启动前：

export LD_LIBRARY_PATH=/hal/lib
export LIBGL_DRIVERS_PATH=/usr/lib/dri
export EGL_LOG_LEVEL=debug

运行：

LD_DEBUG=libs ./cobalt_launcher

你必须看到：

loading /hal/lib/libEGL.so
loading /hal/lib/libGLESv2.so
loading /hal/lib/libgallium-24.3.4.so
loading /usr/lib/dri/swrast_dri.so

不能看到：

/lib/libGLESv2.so
/lib/libEGL.so
九、验证 Mesa 是否真的工作

运行：

strings /hal/lib/libgallium-24.3.4.so | grep Mesa

应该：

Mesa 24.3.4
十、定位 Rasterizer 崩溃地址

你现在：

0xaf446f90

没有符号。

需要：

addr2line -e /hal/lib/libgallium-24.3.4.so 0xaf446f90

但地址是运行时地址。

先：

info proc mappings

找到：

libgallium-24.3.4.so base

比如：

0xaf300000

然后：

python3
>>> hex(0xaf446f90 - 0xaf300000)

得到 offset：

0x146f90

再：

addr2line -f -C \
  -e /hal/lib/libgallium-24.3.4.so \
  0x146f90

就能知道：

崩在哪个 Mesa 函数
十一、推荐调试版 Mesa

重新编译：

-Dbuildtype=debug
-Db_ndebug=false

然后：

export LIBGL_DEBUG=verbose
export MESA_DEBUG=1

Mesa 会打印：

context creation
shader
dispatch
loader

非常有用。

十二、Cobalt 最稳配置

如果只是为了跑：

推荐：

export GALLIUM_DRIVER=llvmpipe

或者：

export LIBGL_ALWAYS_SOFTWARE=1

避免：

Samsung GPU HAL

继续参与。

十三、最可能最终遇到的问题
1. TLS ABI mismatch

Mesa24 修改了：

glapi TLS

旧 loader 会崩。

解决：

必须 frontend/backend 同版本。

2. Wayland buffer ABI mismatch

Samsung tbm 与 Mesa24 gbm 可能不兼容。

解决：

软件渲染。

3. pthread wrapper 崩溃

你日志里的：

__abi_wrap_pthread_cond_wait

已经说明：

Tizen 对 pthread 做了 ABI 包装。

Mesa24 某些线程模型可能不兼容。

解决：

-Dllvm=disabled

非常重要。

十四、真正推荐的方案（生产环境）

实际上：

不要全局替换系统 GLES。

最好：

方法 A（推荐）

只对 Cobalt：

LD_LIBRARY_PATH=/hal/lib ./cobalt_launcher
方法 B

用 chroot/container 单独 Mesa24 runtime。

十五、下一步建议

你现在下一步应该：

1

检查：

readlink -f /lib/libGLESv2.so
readlink -f /hal/lib/libGLESv2.so
2

检查：

LD_DEBUG=libs ./cobalt_launcher 2>&1 | grep GLES
3

检查：

LD_DEBUG=libs ./cobalt_launcher 2>&1 | grep gallium
4

给我：

info proc mappings

我可以直接帮你：

算 crash offset
定位 Mesa 崩溃函数
判断是 loader 崩
还是 glapi 崩
还是 dri driver 崩
