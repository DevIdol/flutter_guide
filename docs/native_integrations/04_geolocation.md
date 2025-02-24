## Location Integration

- **Purpose**: User ရဲ့ တည်နေရာ (GPS) ကို ရယူပြီး location-based services ပေးဖို့။
- **Package**: [geolocator](https://pub.dev/packages/geolocator)
- **Dependency**:
  ```yaml
  dependencies:
    geolocator:
  ```
- **Native Configuration**:
  - Add to `android/gradle.properties`:
    ```
    android.useAndroidX=true
    android.enableJetifier=true
    ```
  - Set compileSdkVersion in `android/app/build.gradle`:
    ```gradle
    android {
        compileSdkVersion 34
        ...
    }
    ```
- **Permissions**:

  - **Android**: `android/app/src/main/AndroidManifest.xml`
    ```xml
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_BACKGROUND_LOCATION" />
    ```
  - **iOS**: `ios/Runner/Info.plist`
    ```xml
    <key>NSLocationWhenInUseUsageDescription</key>
    <string>This app needs access to location when open.</string>
    <key>NSLocationAlwaysUsageDescription</key>
    <string>We need access to your location for better user experience.</string>
    ```
  - Optional iOS Podfile tweak for automatic flag: `ios/Podfile`
    ```ruby
    post_install do |installer|
      installer.pods_project.targets.each do |target|
        if target.name == "geolocator_apple"
          target.build_configurations.each do |config|
            config.build_settings['GCC_PREPROCESSOR_DEFINITIONS'] ||= ['$(inherited)', 'BYPASS_PERMISSION_LOCATION_ALWAYS=1']
          end
        end
      end
    end
    ```
