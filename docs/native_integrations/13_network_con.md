## Network Connectivity

- **Purpose**: Internet connection status (e.g., Wi-Fi, mobile data) ကို စစ်ဆေးပြီး offline/online functionality ပေးဖို့။
- **Package**: [connectivity_plus](https://pub.dev/packages/connectivity_plus)
- **Dependency**:
  ```yaml
  dependencies:
    connectivity_plus:
  ```
- **Permissions**:
  - **Android**: `android/app/src/main/AndroidManifest.xml`
    ```xml
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    ```
  - **iOS**: No additional permissions needed.
