## Camera Integration

- **Purpose**: App ထဲမှာ ဓာတ်ပုံရိုက်ဖို့ သို့မဟုတ် video မှတ်တမ်းတင်ဖို့ camera ကို အသုံးပြုရန်။
- **Package**: [camera](https://pub.dev/packages/camera)
- **Dependency**:
  ```yaml
  dependencies:
    camera:
  ```
- **Permissions**:
  - **Android**: `android/app/src/main/AndroidManifest.xml`
    ```xml
    <uses-permission android:name="android.permission.CAMERA" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    ```
  - **iOS**: `ios/Runner/Info.plist`
    ```xml
    <key>NSCameraUsageDescription</key>
    <string>We need access to your camera to take photos.</string>
    <key>NSMicrophoneUsageDescription</key>
    <string>We need access to your microphone for video recording.</string>
    ```
