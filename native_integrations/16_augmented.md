## AR (Augmented Reality) Integration

- **Purpose**: AR experiences (e.g., virtual objects in real world) ပေးဖို့။
- **Package**: [arcore_flutter_plugin](https://pub.dev/packages/arcore_flutter_plugin) (Android), [ar_flutter_plugin](https://pub.dev/packages/ar_flutter_plugin) (iOS/Android)
- **Dependency**:
  ```yaml
  dependencies:
    arcore_flutter_plugin: ^ # Android only
    ar_flutter_plugin: ^ # Cross-platform option
  ```
- **Permissions**:
  - **Android**: `android/app/src/main/AndroidManifest.xml`
    ```xml
    <uses-permission android:name="android.permission.CAMERA" />
    <uses-feature android:name="android.hardware.camera.ar" android:required="true" />
    ```
  - **iOS**: `ios/Runner/Info.plist`
    ```xml
    <key>NSCameraUsageDescription</key>
    <string>We need camera access for AR features.</string>
    ```
