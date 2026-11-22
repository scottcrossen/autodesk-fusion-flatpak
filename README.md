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
