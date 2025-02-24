## Speech Recognition

- **Purpose**: Voice commands သို့မဟုတ် speech-to-text လုပ်ဖို့။
- **Package**: [speech_to_text](https://pub.dev/packages/speech_to_text)
- **Dependency**:
  ```yaml
  dependencies:
    speech_to_text:
  ```
- **Permissions**:
  - **Android**: `android/app/src/main/AndroidManifest.xml`
    ```xml
    <uses-permission android:name="android.permission.RECORD_AUDIO" />
    <uses-permission android:name="android.permission.INTERNET" />
    ```
  - **iOS**: `ios/Runner/Info.plist`
    ```xml
    <key>NSMicrophoneUsageDescription</key>
    <string>We need microphone access for speech recognition.</string>
    <key>NSSpeechRecognitionUsageDescription</key>
    <string>We need speech recognition to process your voice input.</string>
    ```
