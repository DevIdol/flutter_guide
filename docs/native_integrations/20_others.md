## အောက်ပါ Packages တွေမှာလည်း Native Integrations လိုအပ်ပါတယ်။ package link ပေးထားတဲ့ official doc မှာ ဝင်ရောက်လေ့လာနိုင်ပါတယ်

1. **QR/Barcode Scanning**:

   - **Purpose**: QR codes သို့မဟုတ် barcodes ဖတ်ဖို့။
   - **Package**: [qr_code_scanner](https://pub.dev/packages/qr_code_scanner)

2. **File Picker**:

   - **Purpose**: Device ထဲက files (e.g., PDFs, images) ရွေးဖို့။
   - **Package**: [file_picker](https://pub.dev/packages/file_picker)

3. **Clipboard Access**:

   - **Purpose**: Clipboard ထဲက data ကို read/write ဖို့။
   - **Package**: [flutter_clipboard_manager](https://pub.dev/packages/flutter_clipboard_manager)

4. **Battery Information**:

   - **Purpose**: Battery level သို့မဟုတ် charging status ကို စစ်ဆေးဖို့။
   - **Package**: [battery_plus](https://pub.dev/packages/battery_plus)

5. **App Badges**:

   - **Purpose**: App icon ပေါ်မှာ unread notifications ပြဖို့ badge count ထည့်ရန်။
   - **Package**: [flutter_app_badger](https://pub.dev/packages/flutter_app_badger)

6. **Health Data**:

   - **Purpose**: Health-related data (e.g., steps, heart rate) ကို Google Fit သို့မဟုတ် Apple Health ကနေ read လုပ်ဖို့။
   - **Package**: [health](https://pub.dev/packages/health)

7. **Screen Brightness**:

   - **Purpose**: Device ရဲ့ screen brightness ကို control လုပ်ဖို့။
   - **Package**: [screen_brightness](https://pub.dev/packages/screen_brightness)

8. **Device Local Notification**:

   - **Purpose**: Device Notifications တွေအတွက် သုံးဖို့။
   - **Package**: [flutter_local_notifications](https://pub.dev/packages/flutter_local_notifications)

9. **Custom Native Code**:
   - **Purpose**: Flutter packages တွေမှာ မရှိတဲ့ platform-specific features တွေကို ထည့်ဖို့။
   - **Approach**: Platform Channels နဲ့ Kotlin/Swift သုံးပြီး custom plugins ရေးပါ။

- Project Requirements တွေ အပေါ် မူတည်ပြီး တစ်ခြား Native မှာ Integrate လုပ်ရမယ့် ဟာတွေလည်း ရှိနိုင်ပါသေးတယ်
