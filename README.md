# Autodesk Fusion Flatpak

Install:

```bash
flatpak remote-add --user --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
flatpak install --user flathub org.flatpak.Builder org.freedesktop.Platform//25.08 org.freedesktop.Sdk//25.08 org.freedesktop.Platform.Compat.i386//25.08
git clone https://github.com/scottcrossen/autodesk-fusion-flatpak.git
cd autodesk-fusion-flatpak
flatpak run org.flatpak.Builder --user --install --force-clean build-dir io.github.scottcrossen.AutodeskFusion.yml
flatpak run io.github.scottcrossen.AutodeskFusion
```

The first run downloads and installs Fusion from Autodesk and can take a while; later runs start Fusion directly.

Notes:

- Rendering defaults to software GL. On hosts with a proprietary NVIDIA driver, GPU OpenGL under Wine hangs Fusion's startup (Mesa, the only GL stack a Flatpak ships for the card, cannot drive NVIDIA's kernel module), so the launcher sets `LIBGL_ALWAYS_SOFTWARE=1` unless you override it, e.g. `flatpak override --user --env=LIBGL_ALWAYS_SOFTWARE=0 io.github.scottcrossen.AutodeskFusion` on hardware where GPU rendering works. The embedded Chromium's sandbox is likewise disabled by default (`QTWEBENGINE_DISABLE_SANDBOX=1`); it fails under Wine and blanks the home and sign-in views.
- Sign-in opens in your browser and returns through an `adskidmgr:` link handled by the included `AdskIdentityManager` desktop entry; the launcher passes the link to Autodesk's identity manager instead of starting a second Fusion.
