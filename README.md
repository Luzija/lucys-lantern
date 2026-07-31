# 🏮 Lucy's Lantern

A personal motivational quote app — web-first, now available as a standalone Android app.

> Built with love for Lucia. Light your day.

---

## ✨ Features

- Browse and save motivational quotes
- Favorite quotes for quick access
- Upload custom background images
- Beautiful gradient backgrounds
- Full dark mode support
- **Runs fully offline on Android** — no server required

---

## 📱 Android App

Lucy's Lantern is available as a native Android APK built with [Capacitor](https://capacitorjs.com/).

| Detail | Value |
|---|---|
| App name | Lucy's Lantern |
| Package ID | `online.luciaworld.lucyslantern` |
| APK size | ~4 MB |
| Build type | Debug (personal sideload) |

### Install on Android

1. Download `lucys-lantern-debug.apk` to your phone.
2. Open the APK file. Android will ask you to allow installs from this source — tap **Settings → Allow from this source**, then go back and tap **Install**.
3. Open **Lucy's Lantern** from your app drawer or home screen.

> The "unknown developer" warning is expected. This is a personal debug APK, not Play Store–signed — it is safe for personal use.

### Data persistence on Android

The original web version uses an **Express + SQLite** backend. Since a standalone WebView can't run Node.js, the Android app uses **on-device `localStorage`** instead. Your quotes, favorites, and uploaded backgrounds persist locally on your phone — fully self-contained with no network needed.

For full build and rebuild instructions, see [`docs/APK_HANDOFF.md`](./docs/APK_HANDOFF.md).

---

## 🌐 Web Version

The web version runs the full Express + SQLite stack. Clone and run locally:

```bash
npm install
npm run dev
```

Open [http://localhost:5000](http://localhost:5000).

---

## 🔧 Tech Stack

- **Web:** Node.js · Express · SQLite · TypeScript
- **Android:** Capacitor · WebView shell
- **Frontend:** React (or vanilla JS/TS) · CSS custom properties
- **Icons/splash:** `@capacitor/assets` from PWA icon

---

## 🔄 Updating the Android Build

When the web app changes:

```bash
npm run build
npx cap sync android
cd android && ./gradlew assembleDebug
```

See [`docs/APK_HANDOFF.md`](./docs/APK_HANDOFF.md) for full prerequisites and Android Studio instructions.

---

## 📄 License

Personal project — all rights reserved. Made with 🏮 by Lucia.
