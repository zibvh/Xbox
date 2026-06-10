# Keystore Setup (do this once)

## 1. Generate your keystore
Run this from the `android/` folder:

```bash
keytool -genkey -v -keystore my-release-key.jks \
  -keyalg RSA -keysize 2048 -validity 10000 \
  -alias my-key-alias
```

Enter a password when prompted. Keep the file and password safe —
**losing the keystore means you can never push updates to Play Store.**

## 2. Set your passwords
Either edit `app/build.gradle` directly (not recommended for shared repos),
or set environment variables before building:

```bash
export KEYSTORE_PASSWORD="your_keystore_pass"
export KEY_ALIAS="my-key-alias"
export KEY_PASSWORD="your_key_pass"
./gradlew assembleRelease
```

## 3. Build signed APK
```bash
./gradlew assembleRelease
# Output: app/build/outputs/apk/release/app-release.apk
```

## 4. Play Store — App Signing by Google
When uploading to Play Console for the first time:
- Go to Setup → App Signing
- Let Google manage your signing key (recommended)
- Upload `my-release-key.jks` as your "upload key"

This way even if you lose your keystore, Google can help recover.

## .gitignore reminder
Make sure `my-release-key.jks` is in your `.gitignore` — never commit it.
