## Push Notifications

- **Purpose**: User တွေကို real-time notifications ပို့ပြီး engagement မြှင့်တင်ဖို့။
- **Package**: [firebase_messaging](https://pub.dev/packages/firebase_messaging)
- **Dependency**:
  ```yaml
  dependencies:
    firebase_messaging:
    firebase_core:
  ```
- **Permissions**:
  - **Android**: `android/app/src/main/AndroidManifest.xml`
    ```xml
    <uses-permission android:name="android.permission.INTERNET" />
    ```
  - **iOS**: `ios/Runner/Info.plist`
    ```xml
    <key>UIBackgroundModes</key>
    <array>
        <string>fetch</string>
        <string>remote-notification</string>
    </array>
    <key>FirebaseAppDelegateAutoRegister</key>
    <false/>
    ```
- **Native Configuration**:

  - **Android**: `android/app/build.gradle`
    ```gradle
    apply plugin: 'com.google.gms.google-services'
    dependencies {
        implementation platform('com.google.firebase:firebase-bom:32.3.1')
        implementation 'com.google.firebase:firebase-messaging'
    }
    ```
  - **iOS**: `ios/Runner/AppDelegate.swift`

    ```swift
    import UIKit
    import Firebase
    import FirebaseMessaging

    @UIApplicationMain
    @objc class AppDelegate: FlutterAppDelegate {
        override func application(
            _ application: UIApplication,
            didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?
        ) -> Bool {
            FirebaseApp.configure()
            Messaging.messaging().delegate = self
            GeneratedPluginRegistrant.register(with: self)
            return super.application(application, didFinishLaunchingWithOptions: launchOptions)
        }
    }
    extension AppDelegate: MessagingDelegate {
        // Implement messaging delegate methods if needed
    }
    ```
