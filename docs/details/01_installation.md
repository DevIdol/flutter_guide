## Requirement Installation

- Flutter development စတင်ဖို့ လိုအပ်တဲ့ tools တွေကို အတိုချုပ် ဖော်ပြထားပါတယ်။

### 1. Download Flutter SDK and Setup

- **Purpose**: Flutter framework နဲ့ Dart ကို အသုံးပြုဖို့ SDK ကို စက်ထဲမှာ install လုပ်ပြီး configure လုပ်ရန်။
- **Steps**:
  - Flutter SDK ကို [official website](https://flutter.dev/docs/get-started/install) ကနေ download လုပ်ပြီး local machine မှာ setup လုပ်ပါ။
    - **Windows**: ZIP ဖိုင်ကို extract လုပ်ပြီး `C:sdk\flutter` လို လမ်းကြောင်းတစ်ခုမှာ ထားပါ။
    - **macOS/Linux**: `~/development/flutter` လို လမ်းကြောင်းမှာ extract လုပ်ပါ။
  - Path environment variable ထဲမှာ `flutter/bin` folder ကို ထည့်ပါ:
    - **Windows**: System Settings > Environment Variables > Path ထဲမှာ `C:sdk\flutter\bin` ထည့်ပါ။
    - **macOS/Linux**: `.zshrc` ဒါမှမဟုတ် `.bashrc` ထဲမှာ `export PATH="$PATH:/path/to/flutter/bin"` ထည့်ပြီး `source ~/.zshrc` သို့မဟုတ် `source ~/.bashrc` run ပါ။
  - `flutter doctor -v` run ပြီး dependencies အကုန် အဆင်သင့်ဖြစ်မဖြစ် စစ်ပါ။
    - Output မှာ Android toolchain, Xcode, Chrome (web အတွက်) စတဲ့ လိုအပ်ချက်တွေကို ဖော်ပြပေးမှာဖြစ်ပြီး၊ လိုအပ်တာတွေကို နောက်အဆင့်တွေမှာ ဖြည့်ဆည်းပေးရမှာပါ။
- **Notes**:
  - Flutter ကို Git မှာ clone လုပ်မယ်ဆိုရင် `git clone https://github.com/flutter/flutter.git` သုံးနိုင်ပါတယ်။
  - လမ်းကြောင်းထဲမှာ spaces ပါတဲ့ folder (e.g., `C:\Program Files\flutter`) မထားပါနဲ့၊ build errors ဖြစ်နိုင်ပါတယ်။

### 2. Download Android Studio for Emulator (Windows/macOS)

- **Purpose**: Android app development နဲ့ testing အတွက် Android SDK နဲ့ emulator ပေးတဲ့ Android Studio ကို install လုပ်ရန်။
- **Steps**:
  - Android Studio ကို [official site](https://developer.android.com/studio) ကနေ download လုပ်ပြီး install လုပ်ပါ။
    - **Windows/macOS**: နောက်ဆုံး stable version download လုပ်ပါ။
  - Android Emulator အတွက် AVD (Android Virtual Device) တစ်ခု `Tools > Device Manager` ကနေ create လုပ်ပါ ।
    - **Note**: API level 30+ (e.g., Android 11.0) နဲ့ x86_64 architecture ပါတဲ့ device ရွေးပါ၊ performance ပိုကောင်းပါတယ်။

### 3. Download Xcode for Simulator (macOS)

- **Purpose**: iOS app development နဲ့ testing အတွက် Xcode နဲ့ iOS Simulator ကို macOS မှာ install လုပ်ရန်။
- **Steps**:
  - macOS မှာ iOS Simulator အတွက် Xcode ကို [App Store](https://apps.apple.com/us/app/xcode/id497799835) ကနေ install လုပ်ပါ။
    - **အကြံပြုချက်**: Xcode 15.0+ (iOS 17 support) ကို သုံးပါ။
  - `Xcode > Settings > Platforms` (ဒါမှမဟုတ် အဟောင်း Xcode တွေမှာ `Preferences > Components`) ကနေ Simulator version တွေ (e.g., iOS 17.0) download လုပ်ပါ။
  - Command line tools ကို `xcode-select --install` နဲ့ install လုပ်ပါ။
    - Installed ဖြစ်မဖြစ် စစ်ဖို့ `xcode-select -p` run ပါ။ Output က `/Applications/Xcode.app/Contents/Developer` ဆိုရင် အဆင်ပြေပါတယ်။
  - Simulator ကို `open -a Simulator` နဲ့ ဖွင့်စစ်ပါ။
- **Notes**:
  - macOS ဗားရှင်က Xcode နဲ့ compatible ဖြစ်ဖို့ လိုပါတယ် (e.g., macOS Sonoma 14.0+ က Xcode 15 နဲ့ အဆင်ပြေပါတယ်)။
  - Xcode ကို install လုပ်ပြီးရင် `flutter doctor` run ပြီး iOS toolchain ကို စစ်ပါ။ CocoaPods လိုအပ်ရင် `sudo gem install cocoapods` နဲ့ ထည့်ပါ။

### Additional Requirements

- **Java Development Kit (JDK)**: Android development အတွက် JDK 17+ ကို [Oracle](https://www.oracle.com/java/technologies/javase-jdk17-downloads.html) သို့မဟုတ် [OpenJDK](https://openjdk.java.net/) ကနေ install လုပ်ပြီး `JAVA_HOME` environment variable ထည့်ပါ။
  - **စစ်ဆေးနည်း**: `java -version` run ပါ။
- **Visual Studio Code သို့မဟုတ် IntelliJ IDEA**: Development အတွက် IDE တစ်ခု လိုအပ်ပါတယ်။ VS Code ကို [official site](https://code.visualstudio.com/) ကနေ ရယူနိုင်ပြီး Flutter extension ထည့်ပါ။

- **Notes**:
  - အကယ်၍ web development လုပ်မယ်ဆိုရင် Chrome browser သို့မဟုတ် Edge ကို install လုပ်ထားဖို့ `flutter doctor` က အကြံပြုပါလိမ့်မယ်။

---
