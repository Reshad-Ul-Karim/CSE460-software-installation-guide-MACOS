# Complete Beginner Guide — Install Homebrew, Wine, DSCH2, and Quartus on macOS

This guide explains everything step-by-step for macOS users (Apple Silicon or Intel).

> ⚠️ Important: **DSCH2 and Quartus are Windows software.**
> On macOS, they run using **Wine** (a Windows compatibility layer).

---

# Part 1 — Install Homebrew on macOS

### Step 1 — Open Terminal

Press:

```
Command (⌘) + Space
```

Type **Terminal** → Press **Enter**

---

### Step 2 — Install Xcode Command Line Tools

Run:

```bash
xcode-select --install
```

Click **Install** when prompted.

---

### Step 3 — Install Homebrew

Run:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Enter your macOS password if asked.

---

### Step 4 — Add Homebrew to PATH

Check your Mac type:

```bash
uname -m
```

If you see:

* `arm64` → Apple Silicon
* `x86_64` → Intel

#### Apple Silicon:

```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/opt/homebrew/bin/brew shellenv)"
```

#### Intel:

```bash
echo 'eval "$(/usr/local/bin/brew shellenv)"' >> ~/.zprofile
eval "$(/usr/local/bin/brew shellenv)"
```

---

### Step 5 — Verify Installation

```bash
brew --version
```

Optional check:

```bash
brew doctor
```

---

# Part 2 — Install Wine (Windows Compatibility Layer)

### Step 1 — Update Brew

```bash
brew update
```

### Step 2 — Install Wine Stable

```bash
brew install --cask wine-stable
```

### Step 3 — Verify

```bash
wine --version
```

If a version number appears, Wine is ready.

---

# Part 3 — Download & Extract DSCH2 Software

Software: **DSCH2 (Digital Schematic Editor)**
Download from your Google Drive link.

### Step 1 — Download the ZIP file

Download from:

```
https://drive.google.com/drive/folders/1ucPQLSDH49iYEGfrD6mL07kqLTsqduRR
```

Save it to **Downloads**.

---

### Step 2 — Extract the ZIP File

Open Terminal and run:

```bash
cd ~/Downloads
```

Unzip:

```bash
unzip dsch2.zip
```

Or simply double-click the zip file in Finder.

You can also move it somewhere permanent:

```bash
mkdir -p ~/Applications
mv dsch2 ~/Applications/
```

---

### Step 3 — Run DSCH2

Navigate to the folder:

```bash
cd ~/Applications/dsch2
```

Run:

```bash
wine dsch2.exe
```

(Replace filename if different.)

---

# Part 4 — Install Quartus Software

Software: **Intel Quartus (Windows version)**
Download from:

```
https://drive.google.com/drive/folders/1SfE3-PhhW4R9b9dRB4WuJ_NyL1f8pUKi
```

---

## Step 1 — Extract Quartus ZIP

```bash
cd ~/Downloads
unzip quartus.zip
```

Move it:

```bash
mv quartus ~/Applications/
```

---

## Step 2 — Run Quartus Installer

Navigate to installer folder:

```bash
cd ~/Applications/quartus
```

Run installer using Wine:

```bash
wine setup.exe
```

(Replace with correct installer filename if different.)

---

## Step 3 — Quartus Installation Process

During installation:

1. Click **Next**
2. Accept License Agreement
3. Choose Installation Directory
   Default is usually:

   ```
   C:\intelFPGA\20.x\
   ```

   Leave default unless instructed otherwise.
4. Select Components (keep default selections)
5. Click **Install**
6. Wait (may take 10–30 minutes)
7. Click **Finish**

---

# Part 5 — Locate Quartus Installation Directory (Inside Wine)

Wine stores Windows "C:" drive here:

```
~/.wine/drive_c/
```

Quartus will usually be installed at:

```
~/.wine/drive_c/intelFPGA/
```

Go there:

```bash
cd ~/.wine/drive_c/intelFPGA
```

Then:

```bash
cd 20.1/quartus/bin
```

(Version number may vary.)

You should see:

```
quartus.exe
```

---

# Part 6 — Create Alias for Easy Access to Quartus

Instead of typing the full path every time, create an alias.

### Step 1 — Open shell config file

```bash
nano ~/.zshrc
```

### Step 2 — Add this line at bottom

```bash
alias quartus='wine ~/.wine/drive_c/intelFPGA/20.1/quartus/bin/quartus.exe'
```

(Adjust version if different.)

### Step 3 — Save & Exit

Press:

```
CTRL + X
Y
Enter
```

### Step 4 — Reload Terminal

```bash
source ~/.zshrc
```

---

### Step 5 — Launch Quartus Easily

Now simply type:

```bash
quartus
```

And it will start.

---

# Common Issues & Fixes

### Issue: brew not found

Re-run PATH setup step.

---

### Issue: macOS blocks Wine

Go to:

```
System Settings → Privacy & Security
```

Click **Open Anyway**

---

### Issue: Wine graphical issues

Install winetricks:

```bash
brew install winetricks
```

---

# Final Folder Structure Overview

```
~/Applications/
    ├── dsch2/
    └── quartus/

~/.wine/drive_c/
    └── intelFPGA/
        └── 20.x/
            └── quartus/
                └── bin/
                    └── quartus.exe
```

---

# You Are Done 🎉

You now have:

* Homebrew installed
* Wine installed
* DSCH2 running
* Quartus installed
* Quartus alias created for easy access

---
