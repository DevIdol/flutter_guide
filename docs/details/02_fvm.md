## FVM (Flutter Version Management)

FVM က long-term project တွေမှာ Flutter version ကို ထိန်းချုပ်ဖို့ အထောက်အကူဖြစ်ပြီး team နဲ့ အလုပ်လုပ်တဲ့အခါ မရှိမဖြစ် လိုအပ်ပါတယ်။

#### 1. Installation

- **Windows**:
  - Chocolatey မရှိရင် [chocolatey.org](https://chocolatey.org/install) ကနေ install လုပ်ပါ။
  - Install Chocolatey with PowerShell:
    ```shell
    Set-ExecutionPolicy Bypass -Scope CurrentUser; iwr https://chocolatey.org/install.ps1 -UseBasicParsing | iex
    ```
  - `choco install fvm`
- **macOS**:
  - `curl -fsSL https://fvm.app/install.sh | bash`
- **Pub (All OS)**:
  - `dart pub global activate fvm`
  - **Note**: Global Flutter ကို FVM နဲ့ မထိန်းချင်ရင် ဒီနည်းကို ရှောင်ပါ။

#### 2. Configuration

1. **Install Desired Flutter Version**: `fvm install 3.24.3` (Latest သုံးချင်ရင် `fvm install stable`)
2. **Create Flutter Project**: `flutter create my_project`
3. **Set Project Version**: Project root မှာ `fvm use 3.24.3` run ပါ။
4. **Run Commands with FVM**:
   - Add Package: `fvm flutter pub add package_name`
   - Get Dependencies: `fvm flutter pub get`
   - Run Project: `fvm flutter run`

---
