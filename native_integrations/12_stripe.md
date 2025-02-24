## Payment Gateways (Stripe Integration)

- **Purpose**: Stripe ကို သုံးပြီး secure နဲ့ seamless payment experiences (e.g., cards, Apple Pay, Google Pay) ပေးဖို့။
- **Package**: [flutter_stripe](https://pub.dev/packages/flutter_stripe)
- **Dependency**:
  ```yaml
  dependencies:
    flutter_stripe:
  ```
- **Native Configuration**:

  - **Android**:

    - `android/app/src/main/AndroidManifest.xml`
      - Google Pay သုံးမယ်ဆိုရင် meta-data ထည့်ပါ။
        ```xml
        <application>
            <meta-data
                android:name="com.google.android.gms.wallet.api.enabled"
                android:value="true" />
        </application>
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

  - **iOS**:
    - iOS 13.0+ ကို target လုပ်ပါ။ `ios/Podfile`
      ```ruby
      platform :ios, '13.0'
      ```
    - Apple Pay သုံးမယ်ဆိုရင် `ios/Runner/Info.plist` မှာ ထည့်ပါ။
      ```xml
      <key>CFBundleURLTypes</key>
      <array>
          <dict>
              <key>CFBundleURLSchemes</key>
              <array>
                  <string>stripe-yourapp</string>
              </array>
          </dict>
      </array>
      ```

- **Notes**:
  - Stripe အတွက် server-side endpoint တစ်ခု (e.g., Node.js) လိုအပ်ပြီး PaymentIntent ကို client-side မှာ မလုပ်နိုင်ပါ။
