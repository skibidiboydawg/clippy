# Clippy

Clippy is a small desktop game clip recorder for Windows. It keeps a rolling video buffer in memory-backed disk segments, lets you save the last 5–300 seconds with one key, and uploads clips to Catbox when you want to share them.

It is a native app: Rust with `eframe`/`egui` for the interface and a C++ capture/encode engine. There is no browser runtime, Electron, Node, or WebView2.

## Features

- Rolling buffer that starts with the app. Default hotkey is `F5`; clips are written to `%LOCALAPPDATA%\clippy\clips`.
- GPU encoder selection through DXGI: NVIDIA NVENC, AMD AMF, Intel QSV, with x264 as a fallback.
- Desktop capture with FFmpeg `ddagrab` on D3D11, plus a GDI fallback if DXGI capture is lost.
- System audio via WASAPI loopback, optional microphone input, per-app volume sliders, and a default microphone resolved from Windows.
- CLIPS tab with thumbnails, an in-app player, and buttons to play, upload, or delete a clip.
- Catbox-only uploads with progress, speed, and ETA. Links are copied to the clipboard when auto-upload is enabled.
- Foreground-game detection for clip filenames and Discord Rich Presence. Known games get built-in artwork; no Discord setup is needed.
- Optional update checker against the public `skibidiboydawg/clippy` releases repository.

## Requirements

To run a released build:

- Windows 10 or 11, 64-bit
- FFmpeg 9.x from the gyan.dev full build (the installer handles this)

To build from source:

- Rust toolchain from rustup
- Visual Studio Build Tools 2022 with the C++ workload and Windows SDK
- CMake
- FFmpeg 9.x in `bin\ffmpeg.exe`, or let the installer fetch it

## Build

```powershell
cargo build --release
powershell -ExecutionPolicy Bypass -File build.ps1
```

The first command builds the Rust app and C++ engine. The second packages the installer, `clippy-setup.exe`.

## Use

1. Start Clippy. The buffer begins recording immediately.
2. Play your game. Press `F5` (or your configured hotkey) to save the last few seconds.
3. Open the CLIPS tab to watch, upload, or delete the clip.

Change the hotkey by clicking the `SAVE HOTKEY` button and pressing a new key or combination. Toggle the microphone, audio sources, Discord presence, and update settings in the RECORDER tab.

## Files

Configuration, rolling segments, and clips live under `%LOCALAPPDATA%\clippy`:

```text
config.json
segments\
clips\
```

Only old rolling segments are deleted automatically. Saved clips stay until you remove them.

## Licenses

Bundled JetBrains Mono is licensed under the SIL Open Font License; see `assets\fonts\OFL.txt`. The save sound comes from Kenney Interface Sounds (CC0); see `assets\sounds\clip_bell.SOURCE.txt` and `assets\sounds\KENNEY-LICENSE.txt`.
