## App Widgets/Shortcuts

- **Purpose**: Home screen widgets (Android) သို့မဟုတ် app shortcuts (iOS) ထည့်ပြီး quick access ပေးဖို့။
- **Package**: [home_widget](https://pub.dev/packages/home_widget)
- **Dependency**:
  ```yaml
  dependencies:
    home_widget:
  ```
- **Permissions**:
  - **Android**: `android/app/src/main/AndroidManifest.xml`
    ```xml
    <receiver android:name="com.example.yourapp.WidgetProvider" android:exported="true">
        <intent-filter>
            <action android:name="android.appwidget.action.APPWIDGET_UPDATE" />
        </intent-filter>
        <meta-data
            android:name="android.appwidget.provider"
            android:resource="@xml/widget_info" />
    </receiver>
    ```
  - **iOS**: No specific permissions, but custom intents လိုရင် native Swift code လိုအပ်နိုင်ပါတယ်။
