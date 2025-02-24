## App Links

- **Purpose**: Web URLs (e.g., https://example.com) ကနေ app ကို ဖွင့်ပြီး seamless navigation ပေးဖို့။
- **Package**: [app_links](https://pub.dev/packages/app_links)
- **Dependency**:
  ```yaml
  dependencies:
    app_links:
  ```
- **Permissions**:
  - **Android**: `android/app/src/main/AndroidManifest.xml`
    ```xml
    <meta-data android:name="flutter_deeplinking_enabled" android:value="true" />
    <activity android:name=".MainActivity" android:exported="true">
        <intent-filter android:autoVerify="true">
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="https" android:host="www.example.com" android:pathPrefix="/foo" />
        </intent-filter>
    </activity>
    ```
  - **iOS**: `ios/Runner/Info.plist`
    ```xml
    <key>FlutterDeepLinkingEnabled</key>
    <true/>
    ```
