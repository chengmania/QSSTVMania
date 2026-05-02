# QSSTVMania

**QSSTVMania** is a modernized fork of [QSSTV by Johan Maes (ON4QZ)](https://github.com/ON4QZ/QSSTV), a program for receiving and transmitting SSTV and HAMDRM (sometimes called DSSTV). It is compatible with most of MMSSTV and EasyPal.

Maintained by **Greg Cheng — KC3SMW**
🔗 https://github.com/chengmania/QSSTVMania

---

## What's New in QSSTVMania 9.5.12 (April 2026)

### 🎨 UI Refresh
- Full dark flat theme with ham radio green accent color
- Clean monochrome SVG toolbar icons (Start, Stop, Resync, Save, Erase)
- Green-bordered RX image panel with dark background
- Improved settings panel spacing and layout
- Modern splash screen with callsign and fork attribution
- Styled tab bar, menus, scrollbars, and controls

### 🐛 RX Dropout Bug Fix
- Fixed mid-image decode freeze when receiving over FM repeaters
- Increased sync loss tolerance across all sensitivity levels so brief audio dropouts (PTT gaps, repeater tails, FM audio processing) no longer permanently stall the decoder
- Decoder now recovers and continues decoding after short signal interruptions

### 🏷️ Rebranding
- Application renamed to QSSTVMania
- Version bumped to 9.5.12
- Default image/audio directories updated to `~/qsstvmania/`
- Updated About dialog and splash screen with fork attribution

---

## Installing on Linux (Step-by-Step for Beginners)

Don't worry if you've never compiled software before — these instructions walk you through every step. This works on **Ubuntu, Linux Mint, Debian**, and most other Debian-based distros.

### What You'll Need
- A computer running Linux (Ubuntu 20.04 or newer recommended)
- An internet connection
- About 10–15 minutes

---

### Step 1 — Open a Terminal

Press **Ctrl + Alt + T** on your keyboard. A black or dark window will appear — that's the terminal. You'll type commands here and press **Enter** after each one.

> **Tip:** When you see a command in a grey box like this, type it exactly as shown (or copy and paste it) and press Enter.

---

### Step 2 — Download the Source Code

If you have `git` installed, run:

```bash
git clone https://github.com/chengmania/QSSTVMania.git
```

Then move into the project folder:

```bash
cd QSSTVMania
```

If you don't have git, you can download a ZIP from the GitHub page and unzip it instead.

---

### Step 3 — Install Required Libraries

QSSTVMania needs some helper programs (called dependencies) installed before it can be built. Copy and paste this entire block into your terminal and press Enter:

```bash
sudo apt install pkg-config g++ libfftw3-dev \
  qtbase5-dev qtchooser qt5-qmake qtbase5-dev-tools \
  libqt5svg5-dev libhamlib++-dev libasound2-dev \
  libpulse-dev libopenjp2-7 libopenjp2-7-dev \
  libv4l-dev build-essential
```

Your computer will ask for your **password** (the same one you use to log in). Type it and press Enter — you won't see any characters appear as you type, that's normal.

When it finishes, you'll be back at the prompt.

---

### Step 4 — Create a Build Folder

Run these two commands one at a time:

```bash
mkdir src/build
```

```bash
cd src/build
```

This creates a temporary workspace where the program gets compiled, keeping the source folder clean.

---

### Step 5 — Configure the Build

```bash
qmake ..
```

You should see several lines of output ending with something like `Project MESSAGE: ...`. That means it worked.

---

### Step 6 — Compile the Program

```bash
make -j$(nproc)
```

This is the step that actually builds the program. It may take a few minutes depending on your computer. You'll see lots of text scroll by — that's normal. Wait for it to finish and return to the prompt.

> **What does `-j$(nproc)` mean?** It tells the compiler to use all your CPU cores at once to go faster. Your system figures out how many you have automatically.

---

### Step 7 — Install the Program

```bash
sudo make install
```

Enter your password again if asked. This copies the finished program to the right place on your system so you can launch it from your applications menu.

---

### Step 8 — Launch QSSTVMania

You can now start the program by typing:

```bash
qsstvmania
```

Or search for **QSSTVMania** in your applications menu.

---

### Something Went Wrong?

- **"command not found" after `qmake`** — Re-run Step 3 to make sure all dependencies installed successfully.
- **Errors during `make`** — See the [Debug Compile](#debug-compile) section below and note the exact error message.
- **Program doesn't start** — Make sure PulseAudio is running: `pulseaudio --start`

---

## macOS Installation

For macOS users, install dependencies using [Homebrew](https://brew.sh):

```bash
brew install qt@5 fftw hamlib openjpeg pulseaudio qwt pkg-config
```

Start PulseAudio (required for sound):

```bash
brew services start pulseaudio
```

Then build and install:

```bash
mkdir src/build && cd src/build
/opt/homebrew/opt/qt@5/bin/qmake ..
make -j$(nproc)
sudo make install
```

---

## Debug Compile

If you have problems compiling the software, please provide:

- Linux Distribution and Version (e.g. Ubuntu 22.04)
- Qt Version (e.g. Qt 5.15.3)
- Full output of the compile process showing the error

To compile with debug symbols, first install the required tools:

```bash
sudo apt-get install doxygen libqwt-qt5-dev
```

Then either open `qsstv.pro` in **QtCreator** as a new project, or run:

```bash
qmake CONFIG+=debug
make -j$(nproc)
```

You can then use an external debugger such as `gdb`.

---

## Original Project

QSSTVMania is forked from **QSSTV** by Johan Maes (ON4QZ).

- Original repository: https://github.com/ON4QZ/QSSTV
- Original documentation: https://www.qsl.net/o/on4qz/qsstv/manual
- HAMDRM software based on RX/TXAMADRM by PA0MBO

---

## License

This program is free software; you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation; either version 2 of the License, or (at your option) any later version.
