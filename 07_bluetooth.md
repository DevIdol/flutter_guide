## Bluetooth Integration

- **Purpose**: Bluetooth devices (e.g., wearables, sensors) နဲ့ connect လုပ်ပြီး data တွေကို share လုပ်ဖို့။
- **Package**: [flutter_blue_plus](https://pub.dev/packages/flutter_blue_plus)
- **Dependency**:
  ```yaml
  dependencies:
    flutter_blue_plus:
  ```
- **Permissions**:
  - **Android**: `android/app/src/main/AndroidManifest.xml`
    - Without Location:
      ```xml
      <uses-feature android:name="android.hardware.bluetooth_le" android:required="false" />
      <uses-permission android:name="android.permission.BLUETOOTH_SCAN" android:usesPermissionFlags="neverForLocation" />
      <uses-permission android:name="android.permission.BLUETOOTH_CONNECT" />
      <uses-permission android:name="android.permission.BLUETOOTH" android:maxSdkVersion="30" />
      <uses-permission android:name="android.permission.BLUETOOTH_ADMIN" android:maxSdkVersion="30" />
      <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" android:maxSdkVersion="28" />
      ```
    - With Fine Location:
      ```xml
      <uses-feature android:name="android.hardware.bluetooth_le" android:required="false" />
      <uses-permission android:name="android.permission.BLUETOOTH_SCAN" />
      <uses-permission android:name="android.permission.BLUETOOTH_CONNECT" />
      <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
      <uses-permission android:name="android.permission.BLUETOOTH" android:maxSdkVersion="30" />
      <uses-permission android:name="android.permission.BLUETOOTH_ADMIN" android:maxSdkVersion="30" />
      <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" android:maxSdkVersion="28" />
      ```
  - **iOS**: `ios/Runner/Info.plist`
    ```xml
    <key>NSBluetoothAlwaysUsageDescription</key>
    <string>This app needs Bluetooth to connect to your devices.</string>
    <key>UIBackgroundModes</key>
    <array>
        <string>bluetooth-central</string>
    </array>
    ```
