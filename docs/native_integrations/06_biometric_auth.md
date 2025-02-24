## Biometric Authentication

- **Purpose**: Fingerprint သို့မဟုတ် Face ID ကို သုံးပြီး secure authentication ပေးဖို့။
- **Package**: [local_auth](https://pub.dev/packages/local_auth)
- **Dependency**:
  ```yaml
  dependencies:
    local_auth:
  ```
- **Permissions**:

  - **Android**: `android/app/src/main/AndroidManifest.xml`

    ```xml
    <uses-permission android:name="android.permission.USE_BIOMETRIC" />
    ```

    - MainActivity ကို `FlutterFragmentActivity` အဖြစ် ပြောင်းပါ။ `android/app/src/main/kotlin/com/example/yourapp/MainActivity.kt`

      ```kotlin
      import io.flutter.embedding.android.FlutterFragmentActivity

      class MainActivity: FlutterFragmentActivity() {
          // No additional code needed
      }
      ```

    - Theme ကို `Theme.AppCompat` သုံးပါ။ `android/app/src/main/res/values/styles.xml`
      ```xml
      <resources>
          <style name="LaunchTheme" parent="Theme.AppCompat.DayNight">
              <!-- Customize your theme -->
          </style>
      </resources>
      ```

  - **iOS**: `ios/Runner/Info.plist`
    ```xml
    <key>NSFaceIDUsageDescription</key>
    <string>We need access to Face ID for secure authentication.</string>
    ```
