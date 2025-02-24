## Dart Define Integration

Dart Define ကနေ environment variables (Eg: `APP_NAME`, `APP_SUFFIX`) တွေကို Android နဲ့ iOS မှာ သတ်မှတ်ဖို့ အောက်ပါ native code တွေကို ထည့်ပေးပါ။

---

### Android Integration

#### 1. `android/app/build.gradle` File

အောက်ပါ code ကို `android/app/build.gradle` ဖိုင်ထဲမှာ ထည့်ပါ။

```gradle
def dartEnvironmentVariables = [:]
if (project.hasProperty("dart-defines")) {
    def dartDefines = project.property("dart-defines").split(',')
    dartDefines.each { define ->
        def keyValue = new String(define.decodeBase64()).split('=')
        dartEnvironmentVariables[keyValue[0]] = keyValue[1]
    }
}

android {
    ...

    defaultConfig {
        applicationId "com.example.project"

        // config ထဲက APP_SUFFIX
        applicationIdSuffix dartEnvironmentVariables.get("APP_SUFFIX", "")

        minSdkVersion flutter.minSdkVersion
        targetSdkVersion flutter.targetSdkVersion
        versionCode flutter.versionCode
        versionName flutter.versionName

        // config ထဲက APP_NAME && Fallback အနေနဲ့ default ထည့်ထားပေးပါ
        resValue "string", "app_name", dartEnvironmentVariables.get("APP_NAME", "Default App Name")
    }

    signingConfigs {
        ...
    }
}
```

#### 2. `android/app/src/main/AndroidManifest.xml` File

`android/app/src/main/AndroidManifest.xml` ဖိုင်ထဲမှာ အောက်ပါအတိုင်း သတ်မှတ်ပါ။ `app_name` က `build.gradle` က `resValue` နဲ့ ချိတ်ထားပါတယ်။

```xml
<application
    android:label="@string/app_name"
    android:icon="@mipmap/ic_launcher">
    <!-- Other configurations -->
</application>
```

---

### iOS Integration

iOS မှာ Dart Define ကနေ environment variables တွေကို သတ်မှတ်ဖို့ `Info.plist` နဲ့ Xcode Build Phase script ကို သုံးပါမယ်။

#### 1. `ios/Runner/Info.plist` File

`ios/Runner/Info.plist` ဖိုင်ထဲမှာ အောက်ပါအတိုင်း ထည့်ပါ။

```xml
<key>CFBundleName</key>
<string>$(APP_NAME)</string>
```

- **Note**: `CFBundleDisplayName` အစား `CFBundleName` ကို သုံးတာက ပိုမှန်ပါတယ်။ `CFBundleName` က app icon အောက်က နာမည်ကို ထိန်းတယ်။

#### 2. Xcode Build Phase Script

Xcode မှာ Build Phase script တစ်ခု ထည့်ပြီး `DART DEFINES` ကနေ `APP_NAME` ကို ဖတ်ပါ။

- **Steps**:
  1. Xcode မှာ `Runner` target ကို ဖွင့်ပါ။
  2. `Build Phases` ထဲမှာ "+ New Run Script Phase" ကို နှိပ်ပြီး script ထည့်ပါ။
  3. Script တွင် အောက်ပါ code ကို ထည့်ပါ

```bash
#!/bin/sh

if [ -n "$DART_DEFINES" ]; then
    DART_DEFINES_DECODED=$(echo "$DART_DEFINES" | base64 --decode)
    APP_NAME=$(echo "$DART_DEFINES_DECODED" | grep -o "APP_NAME=[^,]*" | cut -d'=' -f2)
    if [ -z "$APP_NAME" ]; then
        APP_NAME="Default App Name" # Fallback အနေနဲ့ default ထည့်ထားပေးပါ
    fi
    /usr/libexec/PlistBuddy -c "Set :CFBundleName $APP_NAME" "$TARGET_BUILD_DIR/$INFOPLIST_PATH"
fi
```

- **Note**: ဒီ script က `DART DEFINES` ကို decode လုပ်ပြီး `APP_NAME` ကို `Info.plist` ထဲမှာ ထည့်ပေးပါတယ်။

---

### Dart Define ကို အသုံးပြုပြီး Run (OR) Build လုပ်ဖို့

Dart Define ကို အသုံးပြုပြီး Flutter project ကို run ဖို့ ဒါမှမဟုတ် build ဖို့ အောက်ပါ command တွေကို သုံးပါ။

- **Run**:

  ```bash
  fvm flutter run --dart-define-from-file=config.dev.json
  ```

- **Build Android**:

  ```bash
  fvm flutter build apk --dart-define-from-file=config.dev.json
  ```

- **Build iOS**:
  ```bash
  fvm flutter build ios --dart-define-from-file=config.dev.json
  ```

---
