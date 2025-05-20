# Kali-LinuxSetup

Installing Kali Linux on Windows 11 (WSL2)  
How I successfully set up Kali Linux after running into common install errors most tutorials skip.

---

> ⚠️ **Getting this error right after installing Kali from the Microsoft Store?**
> ```
> WslRegisterDistribution failed with error: 0x80004005
> ```
> If you are, you're not alone — I got the same thing.  
> Nothing showed up in `wsl --list --verbose`, and Kali wouldn't launch at all.  
> If this happens, skip straight to [Fixing the Error](#fixing-wslregisterdistribution-error-0x80004005) to save yourself time.

---

## 🛠 What I Used

- Windows 10/11  
- Windows Subsystem for Linux (WSL2)  
- Kali Linux (via Microsoft Store)  
- PowerShell (run as administrator)

---

## 📋 Make Sure You're Running the Latest Windows Version

If you're unsure, press `Win + R`, type `winver`, and press Enter.

![winver](https://github.com/user-attachments/assets/1bf798e3-40ea-4bff-9a74-6ae0de3ffbb5)

If you're not up to date, search for "Update" in the Start menu and install all available updates.

---

## 📥 Downloading and Installing Kali Linux

### Step 1: Open PowerShell as Administrator
Search "PowerShell" from the Start Menu → Right click → "Run as administrator"

### Step 2: Enable Required WSL Features
```powershell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
Enable-WindowsOptionalFeature -Online -FeatureName VirtualMachinePlatform
```

When prompted, restart your PC.

![Enable WSL](https://github.com/user-attachments/assets/1fdfc0bd-816f-48d3-af0c-644ab5659591)

---

## 🔧 Fixing `WslRegisterDistribution` Error (0x80004005)

If after installing Kali from the Microsoft Store it won’t launch, or gives you:

```
WslRegisterDistribution failed with error: 0x80004005
```

Do the following:

1. Open PowerShell as Administrator
2. Run:
   ```powershell
   dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
   dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
   ```
3. Restart your computer
4. Go to [https://aka.ms/wsl2kernel](https://aka.ms/wsl2kernel) and download the kernel update package
5. After installing the kernel update, open PowerShell (Admin) again and run:
   ```powershell
   wsl --set-default-version 2
   ```
6. Now install Kali properly using:
   ```powershell
   wsl --install -d kali-linux
   ```

Kali should now launch successfully and ask you to create a username and password.

---

## 🔁 Continue Installation

### Step 3: Set WSL 2 as Your Default (If You Haven’t Yet)
```powershell
wsl --set-default-version 2
```

![Set WSL version](https://github.com/user-attachments/assets/f8768646-4f55-4c1a-9ff4-bfa90ee98e94)

---

### Step 4: Install Kali from Microsoft Store

Search "Kali Linux" in the Store → Click Install  
⚠️ Don't close the store app until it's finished installing.

Once installed, go to Start → Search "Kali Linux" → Open it.

![Kali install](https://github.com/user-attachments/assets/af02e22c-cb48-4cd9-9f18-88d9c94935da)

---

### Step 5: Set Your Username & Password

Once Kali opens, it will prompt you to create a UNIX username and password.  
Set something memorable — this is what you'll use inside the Kali terminal.

---

## 🎓 Lessons Learned

- Installing Kali from the Store **won’t work** unless WSL 2 is fully set up first.
- PowerShell (run as admin) is the most reliable way to fix WSL issues.
- If you get the `0x80004005` error, don’t panic — it’s super common, and now you know how to fix it.

---

Let me know if this helped you — I made this because no video covered the full process cleanly.
