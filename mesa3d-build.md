### build and run mesa3d


if meson's version is low:sudo pip3 install --upgrade meson


git clone https://gitlab.freedesktop.org/mesa/mesa.git
cd mesa/
meson setup builddir/ --prefix=/home/zzb/workspace/mesa/out --buildtype=debug -Dgallium-drivers=virgl,zink,swrast -Dvulkan-drivers=
sudo meson compile -C builddir/
sudo chown -R $USER:$USER builddir/
sudo meson install -C builddir/



export LD_LIBRARY_PATH=/home/zzb/workspace/mesa/out/lib/x86_64-linux-gnu/dri:/home/zzb/workspace/mesa/out/lib/x86_64-linux-gnu:$LD_LIBRARY_PATH
gdb ../gles-streaming/thirdparty/glfw/out/examples/triangle-opengles





optional:
export LIBGL_DRIVERS_PATH=/home/zzb/workspace/mesa/out/lib/x86_64-linux-gnu/dri:/usr/lib/x86_64-linux-gnu/dri
export LIBGL_ALWAYS_SOFTWARE=1

if libdrm version is low ,don't build mesa drm, clone libdrm and build



API Dispatch
1. python脚本mapi_abi.py生成glapi_mapi_tmp.h
2. 在glapi_mapi_tmp.h中定义glapi，TODO. 注意这个文件：by gl_table.py (from Mesa) script
在_mesa_init_dispatch函数中初始化dispatch表
_mesa_Viewport (x=0, y=0, width=640, height=480) at ../src/mesa/main/viewport.c:140
_mesa_UseProgram (program=3) at ../src/mesa/main/shaderapi.c:2272
_mesa_DrawArrays (mode=4, start=0, count=3) at ../src/mesa/main/draw.c:1372


3. 在builddir中的编译脚本定义-DMAPI_ABI_HEADER=\"/home/zzb/workspace/mesa/builddir/src/mapi/es2api/glapi_mapi_tmp.h
4. src/mapi/mapi_tmp.h文件中包含:#include MAPI_ABI_HEADER
5. src/mapi/entry_x86-64_tls.h中包含:#include "mapi_tmp.h"
