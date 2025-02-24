## Audio/Video Playback

- **Purpose**: Audio နဲ့ video ဖိုင်တွေကို ဖွင့်ပြီး multimedia experiences ပေးဖို့။
- **Package**: [just_audio](https://pub.dev/packages/just_audio), [video_player](https://pub.dev/packages/video_player)
- **Dependency**:
  ```yaml
  dependencies:
    just_audio:
    video_player:
  ```
- **Permissions**:
  - **Android**: `android/app/src/main/AndroidManifest.xml`
    ```xml
    <uses-permission android:name="android.permission.INTERNET" />
    ```
  - **iOS**: No additional permissions needed for basic playback.
