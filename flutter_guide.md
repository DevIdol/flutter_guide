# Flutter Development Guide

## 1. Requirement Installation

- Flutter development စတင်ဖို့ လိုအပ်တဲ့ tools တွေကို အတိုချုပ် ဖော်ပြထားပါတယ်။
- **Details**: [docs/details/01_installation](docs/details/01_installation.md)

## 2. FVM (Flutter Version Management)

- FVM က long-term project တွေမှာ Flutter version ကို ထိန်းချုပ်ဖို့ အထောက်အကူဖြစ်ပြီး team နဲ့ အလုပ်လုပ်တဲ့အခါ မရှိမဖြစ် လိုအပ်ပါတယ်။
- **Details**: [docs/details/02_fvm](docs/details/02_fvm.md)

## 3. Flutter CI

- Flutter CI ကို ထည့်သွင်းဖို့ လိုအပ်ပြီး code quality စစ်ဆေးမှုတွေ လုပ်ဖို့ အသုံးဝင်ပါတယ်။
- **Details**: [.github/workflows/ci](.github/workflows/ci.yaml)

## 4. VSCode Settings

- Team နဲ့ အလုပ်လုပ်မှာမို့ VSCode ကို Setting ချိန်ထားဖို့ဖို့ လိုအပ်ပါတယ်။
- **Details**: [.vscode/settings.json](.vscode/settings.json)

## 5. Dart Define

- Dart Define က compile-time မှာ secure ဖြစ်အောင် environment variables တွေ ထည့်ဖို့ အသုံးဝင်ပါတယ်။
- **Details**: [docs/details/05_dart_define.md](docs/details/05_dart_define.md)

## 6. Shorebird

- Shorebird က code push လုပ်ဖို့ အသုံးဝင်ပြီး Play Store/App Store update မလိုပဲ app ကို update လုပ်နိုင်ပါတယ်။[official doc](https://docs.shorebird.dev/)
- **Details**: [.github/workflows/release.yaml](.github/workflows/release.yaml)
- **Limitations**:
  - Native code နဲ့ assets တွေကို update မလုပ်နိုင်ပါဘူး။ Dart code အတွက်ပဲ အလုပ်လုပ်တယ်။

---

## 7. Native Integration in Flutter (Android and iOS)

- flutter version `3.24.1` ကို အခြေခံထားပါတယ် နောက်ပိုင်း vesion change ရင် native integration တွေလည်း ပြောင်းသွားနိုင်ပါတယ်။

1. [Dart Define Integration](./native_integrations/01_dart_define.md)
2. [Google API Key Integration with Dart Define](./native_integrations/02_api_key.md)
3. [Camera Integration](./native_integrations/03_camera.md)
4. [Geolocation Integration](./native_integrations/04_geolocation.md)
5. [Push Notification Integration](./native_integrations/05_push_notification.md)
6. [Biometric Authentication Integration](./native_integrations/06_biometric_auth.md)
7. [Bluetooth Integration](./native_integrations/07_bluetooth.md)
8. [Media Playback Integration](./native_integrations/08_playback.md)
9. [Deep Link Integration](./native_integrations/09_deeplink.md)
10. [App Link Integration](./native_integrations/10_applink.md)
11. [Background Service Integration](./native_integrations/11_background_service.md)
12. [Stripe Payment Integration](./native_integrations/12_stripe.md)
13. [Network Connectivity Integration](./native_integrations/13_network_con.md)
14. [NFC Integration](./native_integrations/14_nfc.md)
15. [Home Widget Integration](./native_integrations/15_home_widget.md)
16. [Accessibility Integration](./native_integrations/16_augmented.md)
17. [Wearables Integration](./native_integrations/17_wearables.md)
18. [Speech Integration](./native_integrations/18_speech.md)
19. [Vibration Integration](./native_integrations/19_vibration.md)
20. [Other Integrations](./native_integrations/20_others.md)

## 8. State Management and Local Storage Recommendations

- **Recommended State Management**:

  - Small app ဆိုရင် **[Provider](https://pub.dev/packages/provider)** ဒါမှမဟုတ် **[GetX](https://pub.dev/packages/get)** က လုံလောက်ပါတယ်။ [MVC](docs/details/08_mvc.md)
  - Medium app ဆိုရင် **[Riverpod](https://pub.dev/packages/flutter_riverpod)** က type safety နဲ့ scalability ပေးပါတယ်။ [MVVM + Repository](docs/details/08_mvvm.md)
  - Large app ဆိုရင် **[Bloc](https://pub.dev/packages/flutter_bloc)** (**[Bloc Official Doc](https://bloclibrary.dev/getting-started/)**) က complex logic ကို ကောင်းကောင်း handle လုပ်နိုင်ပါတယ်။ [Clean Architecture](docs/details/08_clean_architecture.md)
  - Navigation ကို အဓိကထား စီမံချင်ရင် **[Go Router](https://pub.dev/packages/go_router)** ကို သုံးပါ။

- **Recommended Local Storage**:
  - **[GetStorage](https://pub.dev/packages/get_storage)**: GetX နဲ့အတူ သုံးမယ်ဆိုရင် fast ဖြစ်ပြီး simple data အတွက် သင့်တော်ပါတယ်။
  - **[Shared Preferences](https://pub.dev/packages/shared_preferences)**: General-purpose small data storage အတွက် အဆင်ပြေပါတယ်။
  - **[Flutter Secure Storage](https://pub.dev/packages/flutter_secure_storage)**: API keys လို sensitive data အတွက် မဖြစ်မနေ သုံးသင့်ပါတယ်။

---
