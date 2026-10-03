# Apex Circuit - Android guide

The game is `www/index.html`. Capacitor wraps it into a real Android app.

## Option A: Get a test APK without installing anything (easiest)
1. Create a free account at https://github.com and make a new repository.
2. Upload everything in this folder (keep the `.github` folder).
3. Open the repository > Actions tab > "Build Android APK" > Run workflow.
4. When it finishes (about 5-10 minutes), open the run and download the
   `apex-circuit-debug-apk` artifact. Unzip it to get `app-debug.apk`.
5. Copy the APK to your phone, tap it, and allow "Install unknown apps" when asked.

A debug APK is for testing only. Play Store needs a signed release bundle (Option B).

## Option B: Build with Android Studio (needed for Play Store)
1. Install Node.js (LTS) and Android Studio.
2. Change `appId` in `capacitor.config.json` to something unique you own,
   for example `com.rahul.apexcircuit`. It can never change after you publish.
3. In this folder run:

       npm install @capacitor/core @capacitor/android
       npm install -D @capacitor/cli
       npx cap add android
       npx cap sync
       npx cap open android

4. Add landscape lock: in `android/app/src/main/AndroidManifest.xml`, add
   `android:screenOrientation="sensorLandscape"` inside the `<activity ...>` tag.
5. Press Run in Android Studio to test on an emulator or a USB-connected phone.
6. Icon: put a 1024x1024 `icon.png` in an `assets/` folder, then run
       npm install -D @capacitor/assets
       npx capacitor-assets generate --android
7. Build > Generate Signed Bundle / APK > Android App Bundle. Create a keystore
   and BACK IT UP with its passwords. The output is an `.aab` file.

## Publish on Google Play
1. Create a Play Console account (one-time fee, about US$25): https://play.google.com/console
2. Create the app, upload the `.aab` to a testing track first.
3. Fill in the store listing (screenshots, descriptions, 512x512 icon, 1024x500 feature graphic),
   content rating, data safety form, and a privacy policy URL.
4. Check Play Console for current requirements (minimum target API level, and the closed-testing
   rules for newer personal accounts).

## Notes
- All cars, tracks and drivers are fictional. Do not add real brands or people without a licence.
- Progress is saved in the app's local storage on the device.
- The "Bungee" font loads from Google Fonts. Offline it falls back to Impact/sans-serif.
  For a fully offline app, download the font into `www/` and use @font-face.
- To package a different game, replace `www/index.html` with that game's file and update `appName`.
