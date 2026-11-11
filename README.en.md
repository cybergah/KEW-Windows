<p align="center">
  <img src="images/logo.png" width="140" alt="Kew">
</p>

<h1 align="center">KEW for Windows</h1>

<p align="center">
  <b>Anonymous, free video downloader for the desktop (Windows)</b><br>
  YouTube · X · TikTok · Instagram
</p>

<p align="center">
  <img src="https://img.shields.io/badge/license-GPL--3.0-caa64a">
  <img src="https://img.shields.io/badge/platform-Windows-0078d6">
  <img src="https://img.shields.io/badge/Electron-31-47848f">
  <img src="https://img.shields.io/badge/React-18-61dafb">
  <img src="https://img.shields.io/badge/yt--dlp-bundled-ff0033">
</p>

<p align="center">
  <i>By <b>Cybergah Group</b> · <a href="https://cybergah.com">cybergah.com</a> · <a href="README.md">Kurmancî</a></i>
</p>

---

## 📖 What is Kew?

**Kew** (the Kurmanji name of a mountain bird, the *chukar partridge*) is an
**open-source**, **anonymous** and completely **free** video downloader. This
repository is the **Windows version**: the same React interface as the Android
app, running on the desktop with **Electron**.

Extraction and downloading happen on your own computer with **`yt-dlp.exe` +
`ffmpeg.exe`**: **no servers, no tracking, no ads**. Downloaded files go straight
to the **`Downloads\Kew`** folder.

---

## ✨ Features (same as Android)

- 🔗 Paste a link and download: YouTube, X, TikTok, Instagram
- 🎬 YouTube playlists: every video handled separately, with global pause / resume / cancel
- 🎵 Video or audio only (MP3), quality selection (Max/1080/720/480)
- 💾 Saves to `Downloads\Kew`; built-in player + open with the system player
- 🔁 Automatic retry (a failed video is not skipped)
- 🔔 When finished: notification + partridge sound
- 🌍 5 languages (Kurdish, Turkish, Arabic, English, Persian) + RTL support + splash animation

---

## 📱 Screenshots

| Home | Downloads | Player | Settings |
|:---:|:---:|:---:|:---:|
| <img src="images/home.png" width="180"> | <img src="images/downloads.png" width="180"> | <img src="images/player.png" width="180"> | <img src="images/settings.png" width="180"> |

---

## 🏗️ Architecture

```
┌──────────────────────────────────────────────┐
│  Renderer:  React + TypeScript + Vite        │  ← UI (shared with Android)
├──────────────────────────────────────────────┤
│  Electron main (electron/main.cjs)           │  ← window + IPC
│     └─ spawn yt-dlp.exe / ffmpeg.exe         │  ← extraction/download on device
│  preload.cjs  →  window.kew                  │  ← secure bridge (contextBridge)
└──────────────────────────────────────────────┘
```

| Part | Technology |
|---|---|
| UI | React 18, TypeScript, Vite 5 |
| Desktop | Electron 31 |
| Downloading | yt-dlp.exe + ffmpeg.exe |
| Installer | NSIS (`installer.nsi`) |
| License | GPL-3.0-or-later |

---

## 📂 Project layout

```
KEW-WINDOWS/
├─ electron/
│  ├─ main.cjs        # main process: window + IPC (yt-dlp/ffmpeg)
│  └─ preload.cjs     # secure bridge (window.kew)
├─ src/               # React UI (shared with Android)
│  └─ lib/native.ts   # wired to Electron IPC
├─ resources/
│  ├─ icon.ico        # (yt-dlp.exe and ffmpeg.exe are NOT here, see below)
├─ installer.nsi      # installer script (NSIS)
├─ index.html
└─ package.json
```

> **Note:** `yt-dlp.exe` and `ffmpeg.exe` are **not in the repository** because of
> their size. Fetch them before building (see `tools/fetch-resources.ps1`).

---

## 🔨 Build

Requires **Node.js 18+**.

```powershell
# 1) Install packages
npm install

# 2) Fetch the required binaries (yt-dlp.exe + ffmpeg.exe -> resources\)
powershell -ExecutionPolicy Bypass -File tools\fetch-resources.ps1

# 3) Run (development)
npm start          # vite build + electron .
```

### Build the installer (Kew-Setup.exe)
```powershell
# Install NSIS (makensis.exe), then:
makensis installer.nsi
```
Output: `release\Kew-Setup-1.0.0.exe` (installs without admin rights, with Start menu + Desktop shortcuts).

---

## 📥 Install (users)

- Download `Kew-Setup-1.0.0.exe` from [Releases](https://github.com/cybergah8-lang/KEW-Windows/releases/latest), run it, choose a location and install.
- Or run the **portable** version (`release\Kew-win\Kew.exe`) without installing.
- Downloaded files: `C:\Users\<your name>\Downloads\Kew`

---

## ⚑ Privacy and freedom

> Kew collects no personal data, does no tracking and is always free.
> Extraction happens on your device: no servers, no third parties.
> **We work for a free and anonymous internet.** — *Cybergah Group*

---

## 📜 License

**GPL-3.0-or-later**: free software. Use it, study it, share it, improve it.

---

<p align="center">
  <img src="images/logo.png" width="64"><br>
  <b>Cybergah Group</b> · <a href="https://cybergah.com">cybergah.com</a><br>
  <sub>Kew v1.0.0 · © 2026 · Open source · GPL-3.0</sub><br>
  <sub><i>Free as a bird. 🕊️</i></sub>
</p>
