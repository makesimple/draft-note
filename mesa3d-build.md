### build and run mesa3d


if meson's version is low:sudo pip3 install --upgrade meson


git clone https://gitlab.freedesktop.org/mesa/mesa.git
cd mesa/
meson setup builddir/ --prefix=/home/zzb/workspace/mesa/out --buildtype=debug -Dgallium-drivers=virgl,zink,swrast -Dvulkan-drivers=
sudo meson compile -C builddir/
sudo chown -R $USER:$USER builddir/
sudo meson install -C builddir/

export LIBGL_ALWAYS_SOFTWARE=1

export LD_LIBRARY_PATH=/home/zzb/workspace/mesa/out/lib/x86_64-linux-gnu/dri:/home/zzb/workspace/mesa/out/lib/x86_64-linux-gnu:$LD_LIBRARY_PATH
gdb ../gles-streaming/thirdparty/glfw/out/examples/triangle-opengles
