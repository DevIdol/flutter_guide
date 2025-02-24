## NFC (Near Field Communication)

- **Purpose**: Contactless payments သို့မဟုတ် NFC tags ဖတ်ဖို့/ရေးဖို့ (e.g., RFID, transit cards)။
- **Package**: [nfc_manager](https://pub.dev/packages/nfc_manager)
- **Dependency**:
  ```yaml
  dependencies:
    nfc_manager:
  ```
- **Permissions**:
  - **Android**: `android/app/src/main/AndroidManifest.xml`
    ```xml
    <uses-permission android:name="android.permission.NFC" />
    <uses-feature android:name="android.hardware.nfc" android:required="true" />
    ```
  - **iOS**: `ios/Runner/Info.plist`
    ```xml
    <key>NFCReaderUsageDescription</key>
    <string>We need NFC to scan tags.</string>
    <key>com.apple.developer.nfc.readersession.formats</key>
    <array>
        <string>NDEF</string>
        <string>TAG</string>
    </array>
    ```
