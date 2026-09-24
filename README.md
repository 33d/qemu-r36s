# QEMU for Ubuntu Eoan

The GitHub Actions workflow builds the Ubuntu Eoan QEMU source package on a
native `arm64` runner (`ubuntu-24.04-arm`) inside an Eoan `pbuilder` root
filesystem. The source is downloaded with `apt`, and the resulting Debian
packages are published as the `qemu-eoan-arm64` workflow artifact.

The build enables SDL and disables GTK and OpenGL:

```text
--enable-sdl --disable-gtk --disable-opengl
```

This is the closest configuration supported by Ubuntu Eoan's QEMU 4.0
packaging. That QEMU release has no `--disable-x11` option, and its SDL probe
detects SDL's X11 backend and links the system build with X11. Therefore the
artifact is SDL-enabled without GTK/OpenGL, but it is not literally X11-free.
