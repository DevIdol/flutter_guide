## Vibration/Haptics

- **Purpose**: Device vibration သို့မဟုတ် haptic feedback ပေးဖို့။
- **Package**: [vibration](https://pub.dev/packages/vibration)
- **Dependency**:
  ```yaml
  dependencies:
    vibration:
  ```
- **Permissions**:
  - **Android**: `android/app/src/main/AndroidManifest.xml`
    ```xml
    <uses-permission android:name="android.permission.VIBRATE" />
    ```
  - **iOS**: No additional permissions needed.
