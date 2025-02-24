## Deep Linking

- **Purpose**: External links ကနေ app ကို ဖွင့်ပြီး specific content သို့မဟုတ် features ကို ဝင်ရောက်ဖို့။
- **Package**: [uni_links](https://pub.dev/packages/uni_links)
- **Dependency**:
  ```yaml
  dependencies:
    uni_links:
  ```
- **Permissions**:
  - **Android**: `android/app/src/main/AndroidManifest.xml`
    ```xml
    <activity android:name=".MainActivity" android:exported="true">
        <intent-filter>
            <action android:name="android.intent.action.VIEW" />
            <category android:name="android.intent.category.DEFAULT" />
            <category android:name="android.intent.category.BROWSABLE" />
            <data android:scheme="yourapp" android:host="example.com" />
        </intent-filter>
    </activity>
    ```
  - **iOS**: `ios/Runner/Info.plist`
    ```xml
    <key>CFBundleURLTypes</key>
    <array>
        <dict>
            <key>CFBundleURLSchemes</key>
            <array>
                <string>yourapp</string>
            </array>
        </dict>
    </array>
    ```
