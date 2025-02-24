## 1. Requirement Installation

Flutter development စတင်ဖို့ လိုအပ်တဲ့ tools တွေကို အတိုချုပ်ပြီး ပြောပြပေးထားပါတယ်။

1. **Download Flutter SDK and Setup**

   - Flutter SDK ကို [official website](https://flutter.dev/docs/get-started/install) ကနေ download လုပ်ပြီး local machine မှာ setup လုပ်ပါ။
   - Path environment variable ထဲမှာ `flutter/bin` folder ကို ထည့်ပါ (Windows: System Settings > Environment Variables; macOS/Linux: `.zshrc` ဒါမှမဟုတ် `.bashrc` ထဲမှာ `export PATH="$PATH:/path/to/flutter/bin"` ထည့်ပါ)။
   - `flutter doctor` run ပြီး dependencies အကုန် အဆင်သင့်ဖြစ်မဖြစ် စစ်ပါ။

2. **Download Android Studio for Emulator (Windows/macOS)**

   - Android Studio ကို [official site](https://developer.android.com/studio) ကနေ download လုပ်ပြီး install လုပ်ပါ။
   - Android Emulator အတွက် AVD တစ်ခု `Tools > Device Manager` ကနေ create လုပ်ပါ။

3. **Download Xcode for Simulator (macOS)**
   - macOS မှာ iOS simulator အတွက် Xcode ကို [App Store](https://apps.apple.com/us/app/xcode/id497799835) ကနေ install လုပ်ပါ။
   - `Xcode > Preferences > Components` ကနေ simulator version တွေ download လုပ်ပါ။
   - Command line tools ကို `xcode-select --install` နဲ့ install လုပ်ပါ။ **Note**: `open -a Simulator` နဲ့ simulator စစ်ပါ။

---

## 2. FVM (Flutter Version Management)

FVM က long-term project တွေမှာ Flutter version ကို ထိန်းချုပ်ဖို့ အထောက်အကူဖြစ်ပြီး team နဲ့ အလုပ်လုပ်တဲ့အခါ မရှိမဖြစ် လိုအပ်ပါတယ်။

#### 1. Installation

- **Windows**:
  - Chocolatey မရှိရင် [chocolatey.org](https://chocolatey.org/install) ကနေ install လုပ်ပါ။
  - Install Chocolatey with PowerShell:
    ```shell
    Set-ExecutionPolicy Bypass -Scope CurrentUser; iwr https://chocolatey.org/install.ps1 -UseBasicParsing | iex
    ```
  - `choco install fvm`
- **macOS**:
  - `curl -fsSL https://fvm.app/install.sh | bash`
- **Pub (All OS)**:
  - `dart pub global activate fvm`
  - **Note**: Global Flutter ကို FVM နဲ့ မထိန်းချင်ရင် ဒီနည်းကို ရှောင်ပါ။

#### 2. Configuration

1. **Install Desired Flutter Version**: `fvm install 3.24.3` (Latest သုံးချင်ရင် `fvm install stable`)
2. **Create Flutter Project**: `flutter create my_project`
3. **Set Project Version**: Project root မှာ `fvm use 3.24.3` run ပါ။
4. **Run Commands with FVM**:
   - Add Package: `fvm flutter pub add package_name`
   - Get Dependencies: `fvm flutter pub get`
   - Run Project: `fvm flutter run`

---

## 3. Flutter CI

Flutter CI ကို ထည့်သွင်းဖို့ လိုအပ်ပြီး အောက်က အချက်တွေကို စစ်ဆေးပါ။

Eg: `.github/workflows/ci.yaml` [ci.yaml](.github/workflows/ci.yaml)

- **Check FVM Flutter Version**
- **Check Code Format**
- **Check Unit Tests**
- **Additional Checks**:
  - Linting: `fvm flutter analyze`
  - Dependency audit: `fvm flutter pub deps`

## 4. VSCode Settings

Team နဲ့ အလုပ်လုပ်မှာမို့ VSCode ကို ချိန်ဖို့ လိုအပ်ပါတယ်။

- **Extensions**:
  - Flutter, Dart, FVM extensions ထည့်ပါ။
- **Settings**:
  - `.vscode/settings.json` [settings.json](.vscode/settings.json)
- Team တစ်ခုလုံး တူညီတဲ့ settings သုံးဖို့ မမေ့ပါနဲ့။

## 5. Dart Define

Dart Define က compile-time မှာ secure ဖြစ်အောင် environment variables (ဥပမာ: API keys, app name) တွေ ထည့်ဖို့ အသုံးဝင်ပါတယ်။

- **Use Cases**:
  - develop, staging, production အတွက် ခွဲပြီး app name, API keys, base URLs စတာတွေ သတ်မှတ်ဖို့။
- **Example Config**:  
  **File: config.dev.json**
  ```json
  {
    "APP_NAME": "App Name.DEV",
    "APP_SUFFIX": ".dev",
    "API_BASE_URL": "http://172.20.10.5:8080", // Local IP ကို Android emulator အတွက် သုံးပါ။ iOS မှာ `localhost` အလုပ်လုပ်တယ်။
    "GOOGLE_API_KEY": ""
  }
  ```
- **Commands**:
  - **Run**: `fvm flutter run --dart-define-from-file=config.dev.json`
  - **Build Android**: `fvm flutter build apk --dart-define-from-file=config.dev.json`
  - **Build iOS**: `fvm flutter build ios --dart-define-from-file=config.dev.json`
- **Manual API Key**: Config ထဲမထည့်ချင်ရင် CLI ကနေ ထည့်လို့ရပါတယ်။
  - `fvm flutter run --dart-define-from-file=config.dev.json --dart-define=GOOGLE_API_KEY=your_api_key`
- **Native Integration**:
  - `APP_NAME` နဲ့ `GOOGLE_API_KEY` ကို native မှာ ထည့်ဖို့လိုတယ်။

---

## 6. Shorebird

[Shorebird](https://docs.shorebird.dev/) က code push လုပ်ဖို့ အသုံးဝင်ပြီး Play Store/App Store update မလိုပဲ app ကို update လုပ်နိုင်ပါတယ်။
shorebird ကို pipeline create လုပ်ပြီး run လုပ်ဖို့ အကြံပေးချင်ပါတယ်။
Eg: `.github/workflows/release.yaml` [release.yaml](.github/workflows/release.yaml)

- **Limitations**:
  - Native code နဲ့ assets တွေကို update မလုပ်နိုင်ပါဘူး။ Dart code အတွက်ပဲ အလုပ်လုပ်တယ်။

---

### 7. Native Integration in Flutter (Android and iOS)

- flutter version `3.24.1` ကို အခြေခံထားပါတယ် နောက်ပိုင်း vesion ချိန်ရင် native integration တွေလည်း ပြောင်းသွားနိုင်ပါတယ်။

1. [Dart Define Integration](01_dart_define.md)
2. [Google API Key Integration with Dart Define](02_api_key.md)
3. [Camera Integration](03_camera.md)
4. [Geolocation Integration](04_geolocation.md)
5. [Push Notification Integration](05_push_notification.md)
6. [Biometric Authentication Integration](06_biometric_auth.md)
7. [Bluetooth Integration](07_bluetooth.md)
8. [Media Playback Integration](08_playback.md)
9. [Deep Link Integration](09_deeplink.md)
10. [App Link Integration](10_applink.md)
11. [Background Service Integration](11_background_service.md)
12. [Stripe Payment Integration](12_stripe.md)
13. [Network Connectivity Integration](13_network_con.md)
14. [NFC Integration](14_nfc.md)
15. [Home Widget Integration](15_home_widget.md)
16. [Accessibility Integration](16_augmented.md)
17. [Wearables Integration](17_wearables.md)
18. [Speech Integration](18_speech.md)
19. [Vibration Integration](19_vibration.md)
20. [Other Integration](20_others.md)
