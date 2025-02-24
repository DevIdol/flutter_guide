## Google API Key Integration with Dart Define

- API KEY ကို secure ဖြစ်အောင် အသုံးပြုဖို့ အရေးကြီးပါတယ် native code ထဲမှာ တိုက်ရိုက်သွားထည့်တာ မဟုတ်ဘဲ dart define ကို အသုံးပြုပြီး ထည့်လိုက်မယ်ဆိုရင် compile-time မှာ key ကို machine code အဖြစ် ပြောင်းပေးတာကြောင့် တိုက်ရိုက် hardcode လုပ်တာထက် ပိုမို secure ဖြစ်ပါတယ်။ Dart Define က compile-time မှာ key ကို native layer ထဲ ထည့်ပေးတာမို့ source code ထဲမှာ မပေါ်ပါဘူး။

### Android Integration for Google API Key

Android မှာ Google API Key ကို Dart Define ကနေ ဖတ်ပြီး `AndroidManifest.xml` ထဲမှာ အသုံးပြုဖို့ အောက်ပါအဆင့်တွေကို လုပ်ပါ။

#### 1. `android/app/build.gradle` File

`android/app/build.gradle` ဖိုင်ထဲမှာ Dart Define ကနေ `GOOGLE_API_KEY` ကို read လုပ်ဖို့ အောက်ပါ code ကို ထည့်ပါ။

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
        applicationIdSuffix dartEnvironmentVariables.get("APP_SUFFIX", "")
        minSdkVersion flutter.minSdkVersion
        targetSdkVersion flutter.targetSdkVersion
        versionCode flutter.versionCode
        versionName flutter.versionName

        resValue "string", "app_name", dartEnvironmentVariables.get("APP_NAME", "Default App Name")

        resValue "string", "google_api_key", dartEnvironmentVariables.get("GOOGLE_API_KEY", "")
    }

    signingConfigs {
        ...
    }
}
```

#### 2. `android/app/src/main/AndroidManifest.xml` File

`android/app/src/main/AndroidManifest.xml` ဖိုင်ထဲမှာ Google API Key ကို အောက်ပါအတိုင်း meta-data အနေနဲ့ ထည့်ပါ။

```xml
<application
    android:label="@string/app_name"
    android:icon="@mipmap/ic_launcher">
    <!-- Google API Key meta-data -->
    <meta-data
        android:name="com.google.android.geo.API_KEY"
        android:value="@string/google_api_key" />
    <!-- Other configurations -->
</application>
```

- **Note**: `android:value="@string/google_api_key"` က `build.gradle` မှာ သတ်မှတ်ထားတဲ့ `resValue` ကို ချိတ်ဆက်ပြီး Dart Define ကနေ read လုပ်ထားတဲ့ key ကို အသုံးပြုပါတယ်။

---

### iOS Integration for Google API Key

iOS မှာ Google API Key ကို Dart Define ကနေ ဖတ်ပြီး `Info.plist` ထဲမှာ ထည့်ဖို့ Build Phase script ကို သုံးပါမယ်။

#### 1. `ios/Runner/Info.plist` File

`ios/Runner/Info.plist` ဖိုင်ထဲမှာ Google API Key ကို အောက်ပါအတိုင်း ထည့်ပါ။

```xml
<key>CFBundleName</key>
<string>$(APP_NAME)</string>
<!-- Google API Key -->
<key>GoogleAPIKey</key>
<string>$(GOOGLE_API_KEY)</string>
```

#### 2. Xcode Build Phase Script

Xcode မှာ Build Phase script တစ်ခု ထည့်ပြီး `DART DEFINES` ကနေ `GOOGLE_API_KEY` ကို ဖတ်ပါ။

- **Steps**:
  1. Xcode မှာ `Runner` target ကို ဖွင့်ပါ။
  2. `Build Phases` ထဲမှာ "+ New Run Script Phase" ကို နှိပ်ပါ။
  3. Script ကို အောက်ကလို ထည့်ပါ (ရှိပြီးသား script ရှိရင် ဒီ logic ကို ထည့်ပေါင်းပါ)။

```bash
#!/bin/sh

if [ -n "$DART_DEFINES" ]; then
    DART_DEFINES_DECODED=$(echo "$DART_DEFINES" | base64 --decode)
    # APP_NAME အတွက်
    APP_NAME=$(echo "$DART_DEFINES_DECODED" | grep -o "APP_NAME=[^,]*" | cut -d'=' -f2)
    if [ -z "$APP_NAME" ]; then
        APP_NAME="Default App Name"
    fi
    /usr/libexec/PlistBuddy -c "Set :CFBundleName $APP_NAME" "$TARGET_BUILD_DIR/$INFOPLIST_PATH"

    # GOOGLE_API_KEY အတွက်
    GOOGLE_API_KEY=$(echo "$DART_DEFINES_DECODED" | grep -o "GOOGLE_API_KEY=[^,]*" | cut -d'=' -f2)
    if [ -z "$GOOGLE_API_KEY" ]; then
        GOOGLE_API_KEY="YOUR_DEFAULT_API_KEY" # Fallback အနေနဲ့ default key
    fi
    /usr/libexec/PlistBuddy -c "Set :GoogleAPIKey $GOOGLE_API_KEY" "$TARGET_BUILD_DIR/$INFOPLIST_PATH"
fi
```

- **Note**: ဒီ script က `DART DEFINES` ကနေ `GOOGLE_API_KEY` ကို decode လုပ်ပြီး `Info.plist` ထဲမှာ ထည့်ပေးပါတယ်။ `APP_NAME` နဲ့ အတူတူ run အောင် ပေါင်းထည့်ထားပါတယ်။

---

### Config ဖိုင်နဲ့ Run/Build လုပ်နည်း

#### Config ဖိုင် ဥပမာ

`config.dev.json` ဖိုင်ထဲမှာ Google API Key ကို အောက်ပါအတိုင်း ထည့်ပါ။

```json
{
  "APP_NAME": "App Name.DEV",
  "APP_SUFFIX": ".dev",
  "API_BASE_URL": "http://172.20.10.5:8080",
  "GOOGLE_API_KEY": "your_google_api_key_here"
}
```

- **Note**: Sensitive data ဖြစ်တဲ့ `GOOGLE_API_KEY` ကို config ထဲမထည့်ချင်ရင် CLI ကနေ `--dart-define=GOOGLE_API_KEY=your_key` နဲ့ ထည့်လို့လည်း ရပါတယ်။

#### Run သို့မဟုတ် Build Commands

Dart Define ကို အသုံးပြုပြီး project ကို run ဖို့ ဒါမှမဟုတ် build ဖို့ အောက်ပါ command တွေကို သုံးပါ။

- **Run**:

  ```bash
  fvm flutter run --dart-define-from-file=config/config.dev.json
  ```

- **Build Android**:

  ```bash
  fvm flutter build apk --dart-define-from-file=config/config.dev.json
  ```

- **Build iOS**:

  ```bash
  fvm flutter build ios --dart-define-from-file=config/config.dev.json
  ```

- **Manual API Key နဲ့ Run**:
  ```bash
  fvm flutter run --dart-define=GOOGLE_API_KEY=your_actual_google_api_key_here
  ```

---
