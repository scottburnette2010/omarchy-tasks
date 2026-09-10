# Build OBS Studio for AArch64

Build OBS Studio natively on an AArch64 Omarchy system. The browser source
plugin is disabled because OBS's prebuilt CEF bundle is currently published
for x86_64, not AArch64.

## Install build dependencies

Install the dependencies that are not already present:

```bash
sudo pacman -S libdatachannel libjuice librist mbedtls3 qrcodegencpp-cmake rnnoise
```

The remaining OBS build dependencies are available from the configured Arch
repositories.

## Build

Use the AArch64 PKGBUILD from the Omarchy AArch64 package repository:

```bash
git clone https://github.com/omarchy-mac/omarchy-pkgs-aarch64.git
cd omarchy-pkgs-aarch64/pkgbuilds/obs-studio
makepkg -s --noconfirm
```

The resulting package is:

```text
obs-studio-32.2.2-1-aarch64.pkg.tar.xz
```

## Install

Install the package created in the build directory:

```bash
sudo pacman -U obs-studio-32.2.2-1-aarch64.pkg.tar.xz
```

This build includes PipeWire, JACK, PulseAudio, V4L2, WebRTC, VLC, x264,
FDK-AAC, and OBS WebSocket support. It does not include the browser source or
browser dock because no compatible AArch64 CEF package is available.
