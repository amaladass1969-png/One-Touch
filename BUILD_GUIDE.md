# One-Touch AI — Android Build Guide
## Samacheer Kalvi · TN Matriculation · Classes 1–12

---

## METHOD 1 — Android Studio (Easiest) ✅ RECOMMENDED

### Step 1: Install Android Studio
Download from: https://developer.android.com/studio

### Step 2: Open the project
- Open Android Studio
- Click **File → Open**
- Select the `OneTouchAI_Android` folder
- Wait for Gradle sync to complete (~2–5 mins first time)

### Step 3: Build the APK
- Click **Build → Build Bundle(s)/APK(s) → Build APK(s)**
- APK will be at:
  `app/build/outputs/apk/debug/app-debug.apk`

### Step 4: Install on Android device
- Enable **Developer Options** on your Android phone
- Enable **USB Debugging**
- Connect via USB and run:
  ```
  adb install app/build/outputs/apk/debug/app-debug.apk
  ```

---

## METHOD 2 — Command Line (Gradle) ✅

### Prerequisites
- Java JDK 17+: https://adoptium.net
- Android SDK (via Android Studio or standalone)
- Set `ANDROID_HOME` environment variable

### Build Commands
```bash
cd OneTouchAI_Android

# On Mac/Linux
./gradlew assembleDebug

# On Windows
gradlew.bat assembleDebug
```

APK output: `app/build/outputs/apk/debug/app-debug.apk`

### For Release APK (signed)
```bash
./gradlew assembleRelease
```

---

## METHOD 3 — Online APK Builder (No install needed) ✅

### Using ApkOnline.net
1. Go to https://www.apkonline.net/runapk/run-apk-online.html
2. Note: This runs APKs but doesn't build them

### Using Appetize.io
1. Go to https://appetize.io
2. Upload the APK to test on virtual Android device

### Using GitHub Actions (Free CI/CD)
1. Push project to GitHub
2. Add `.github/workflows/build.yml`:
```yaml
name: Build APK
on: [push]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-java@v3
        with:
          java-version: '17'
          distribution: 'temurin'
      - name: Build APK
        run: ./gradlew assembleDebug
      - uses: actions/upload-artifact@v3
        with:
          name: OneTouchAI-debug.apk
          path: app/build/outputs/apk/debug/app-debug.apk
```

---

## APP DETAILS

| Property | Value |
|---|---|
| App Name | One-Touch AI |
| Package | com.onetouchai |
| Min Android | 5.0 (API 21) |
| Target Android | 14 (API 34) |
| Version | 1.0 |
| Internet Required | Yes (for AI generation) |

## FEATURES IN APK
- ✅ All 8 Samacheer Kalvi subjects
- ✅ Classes 1–12 with auto-updating chapter lists
- ✅ Terms 1, 2 & 3
- ✅ AI-powered module generation via Anthropic API
- ✅ 6 learning modules per chapter
- ✅ Full-screen WebView with hardware acceleration
- ✅ Back button navigation support
- ✅ Portrait & landscape support

## PROJECT STRUCTURE
```
OneTouchAI_Android/
├── app/
│   ├── src/main/
│   │   ├── AndroidManifest.xml
│   │   ├── assets/
│   │   │   └── index.html          ← Full One-Touch AI app
│   │   ├── java/com/onetouchai/
│   │   │   └── MainActivity.java   ← WebView host activity
│   │   └── res/
│   │       ├── layout/activity_main.xml
│   │       ├── values/strings.xml
│   │       ├── values/styles.xml
│   │       └── mipmap-*/ic_launcher.png
│   └── build.gradle
├── build.gradle
├── settings.gradle
└── gradle.properties
```
