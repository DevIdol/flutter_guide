## Wearables Integration

- **Purpose**: Smartwatches (e.g., Wear OS, Apple Watch) နဲ့ connect လုပ်ပြီး data sync သို့မဟုတ် controls ပေးဖို့။
- **Package**: No direct Flutter package; requires custom native code or companion apps.
- **Native Setup**:
  - **Android (Wear OS)**: Wear OS app တစ်ခု သီးသန့် လိုအပ်ပြီး `android/app/src/main/AndroidManifest.xml` မှာ companion app ချိတ်ဆက်ဖို့ ထည့်ပါ။
    ```xml
    <meta-data
        android:name="com.google.android.wearable.standalone"
        android:value="true" />
    ```
  - **iOS (watchOS)**: WatchKit extension လိုအပ်ပြီး Xcode မှာ သီးသန့် target ထည့်ရပါမယ်။
