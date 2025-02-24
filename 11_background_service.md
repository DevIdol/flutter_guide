## Background Services

- **Purpose**: App ပိတ်ထားချိန်မှာလည်း background tasks (e.g., location updates) လုပ်ဖို့။
- **Package**: [flutter_background_service](https://pub.dev/packages/flutter_background_service)
- **Dependency**:
  ```yaml
  dependencies:
    flutter_background_service:
  ```
- **Permissions**:
  - **Android**: `android/app/src/main/AndroidManifest.xml`
    ```xml
    <uses-permission android:name="android.permission.FOREGROUND_SERVICE" />
    <application>
        <service
            android:name="id.flutter.flutter_background_service.BackgroundService"
            android:foregroundServiceType="location" />
    </application>
    ```
  - **iOS**: `ios/Runner/Info.plist`
    ```xml
    <key>BGTaskSchedulerPermittedIdentifiers</key>
    <array>
        <string>dev.flutter.background.refresh</string>
    </array>
    <key>UIBackgroundModes</key>
    <array>
        <string>fetch</string>
    </array>
    ```
