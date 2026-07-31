# Lucy's Lantern — Android App Handoff

Lucy's Lantern is now wrapped as a native Android app with [Capacitor](https://capacitorjs.com/).
It installs to the home screen with its own lantern icon and opens **full-screen, with no
browser chrome** (standalone WebView).

## What was produced

| Item | Detail |
|---|---|
| **App name** | Lucy's Lantern |
| **Package ID** | `online.luciaworld.lucyslantern` |
| **APK size** | ~4 MB |
| **Build type** | Debug (sideload / personal use) |
| **Built with** | Capacitor Android |

## Installing the APK on Android (no build needed)

1. Copy `lucys-lantern-debug.apk` to the phone (USB, email, Drive, etc.).
2. On the phone, open the file. Android will prompt to allow installing from this source —
   approve it (**Settings → "Install unknown apps"** for the app you opened it from).
3. Tap **Install**. "Lucy's Lantern" appears in the app drawer with the lantern icon.

> **Note:** The "unknown developer" warning is expected — this is a personal debug APK, not Play Store–signed. That is normal and safe for personal sideloading.

## Offline / data persistence

The original web app stored quotes and backgrounds via an **Express + SQLite** backend.
A plain Android WebView **cannot run Node/Express/better-sqlite3**, so the native build
swaps the network data layer for **on-device `localStorage`**:

- `client/src/lib/localStore.ts` reimplements the exact REST surface the UI uses
  (`GET/POST/PATCH/DELETE /api/quotes` and `/api/backgrounds`), seeded with the same
  default quotes and gradient backgrounds as the server.
- `client/src/lib/queryClient.ts` detects the native runtime (`window.Capacitor`) and routes
  all data ops to the local store. **On the web it is unchanged** and still talks to the
  real Express server.

**Result:** quotes, backgrounds, favorites, and uploaded background images all persist locally
on the phone, fully self-contained with no network or backend required.

> Google Fonts are still loaded from CDN when online; offline they gracefully fall back to system fonts.

## Rebuilding the APK from source

**Prerequisites:** Node 20+, JDK 17+ (full JDK with `jlink`, not a JRE), Android SDK with
`platforms;android-34` and `build-tools;35.0.0`.

```bash
cd motivation-shell
npm install
npm run build            # builds the web app into dist/public
npx cap sync android     # copies web assets + plugins into the android project
cd android
echo "sdk.dir=/path/to/android-sdk" > local.properties
./gradlew assembleDebug  # -> app/build/outputs/apk/debug/app-debug.apk
```

### Via Android Studio

1. `npm install && npm run build && npx cap sync android` (from `motivation-shell/`).
2. Open the `motivation-shell/android` folder in Android Studio.
3. Let Gradle sync, then **Build → Build Bundle(s)/APK(s) → Build APK(s)**,
   or click Run to deploy to a connected device/emulator.

## Icons & splash

Launcher icons and splash screens were generated from the existing PWA lantern icon
(`client/public/icon-512.png`) via `@capacitor/assets` into `android/app/src/main/res/`
(adaptive `mipmap-*` icons + `drawable-*` splash, light bg `#f5ebda` / dark `#171210`).

## Keeping it up to date

Whenever the web app changes, re-run:

```bash
npm run build && npx cap sync android
```

Then rebuild the APK. `cap sync` re-copies `dist/public` into the Android project
and updates native plugins.

## Future: Play Store release

For Play Store distribution, generate a release build signed with your own keystore
rather than the debug key. See the
[Capacitor Android signing docs](https://capacitorjs.com/docs/android/deploying-to-google-play)
for details.
