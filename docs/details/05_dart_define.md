## Dart Define

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
