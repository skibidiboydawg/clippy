# Clippy

Clippy is a small desktop game clip recorder for Windows and Linux. It keeps a rolling video buffer, saves the last 5-300 seconds with one key, and uploads clips to Catbox when you want to share them.

It is a native app. The interface uses Rust with `eframe`/`egui`; Windows uses a C++ capture/encode engine and Linux uses a native Rust FFmpeg backend. There is no browser runtime, Electron, Node, or WebView2.

## Features

- Rolling buffer with a default `F5` hotkey. Saved clips go to `%LOCALAPPDATA%\clippy\clips` on Windows or `~/.local/share/clippy/clips` on Linux.
- Four quality presets: Low (720p30), Medium (720p60), High (1080p60), and Custom (any even resolution, 1-240 FPS, and bitrate).
- GPU encoder selection: NVIDIA NVENC, AMD AMF, Intel QSV, with x264 fallback on Windows; NVENC, VAAPI, QSV, and x264 on Linux.
- Desktop capture with the original D3D11 `ddagrab` path (default) or Windows.Graphics.Capture (`gfxcapture`) on Windows, and X11/XWayland capture on Linux.
- System audio, optional microphone input, per-app volume sliders, and a default microphone resolved from the OS.
- CLIPS tab with thumbnails, an in-app player, and buttons to play, upload, or delete a clip.
- Catbox-only uploads with progress, speed, and ETA. Links are copied to the clipboard when auto-upload is enabled.
- Foreground-game detection for clip filenames and Discord Rich Presence, with built-in artwork for known games.
- Optional update checker against the public `skibidiboydawg/clippy` releases repository.
- Linux install script for Arch, Linux Mint, Ubuntu, Debian, and Pop!_OS, plus an Arch `PKGBUILD`.

## Requirements

Windows:

- Windows 10 or 11, 64-bit
- FFmpeg 9.x from the gyan.dev full build; the installer handles this

Linux:

- x86_64 system with FFmpeg and an X11 or XWayland session
- ALSA, X11, and OpenGL runtime libraries; the install script handles dependencies on supported distros

## Build

Windows:

```powershell
cargo build --release
powershell -ExecutionPolicy Bypass -File build.ps1
```

Linux:

```bash
./linux/install-clippy.sh
```

The Windows commands build the app and package `clippy-setup.exe`. The Linux script installs dependencies, builds `target/release/clippy`, and installs the icon and launcher.

## Use

1. Start Clippy. The buffer begins recording immediately.
2. Play your game. Press `F5`, or your configured hotkey, to save the last few seconds.
3. Open the CLIPS tab to watch, upload, or delete the clip.

Change the hotkey by clicking `SAVE HOTKEY` and pressing a new key or combination. Toggle the microphone, audio sources, Discord presence, and update settings in the RECORDER tab.

## Releases

Download the right asset for your system:

- Windows: `clippy.exe`
- Linux x86_64: `clippy-linux-x86_64.tar.gz`

The Linux archive contains the binary, assets, install script, desktop launcher, and `PKGBUILD`. Extract it, then run `./linux/install-clippy.sh` from the extracted folder.

## Files

Configuration, rolling segments, and clips live under `%LOCALAPPDATA%\clippy` on Windows and `~/.local/share/clippy` on Linux. Only old rolling segments are deleted automatically; saved clips stay until you remove them.

## Licenses

Bundled JetBrains Mono is licensed under the SIL Open Font License; see `assets/fonts/OFL.txt`. The save sound comes from Kenney Interface Sounds (CC0); see `assets/sounds/clip_bell.SOURCE.txt` and `assets/sounds/KENNEY-LICENSE.txt`.
