# MB9i ZMK Configuration

This repository contains the ZMK firmware configuration for the **MB9i**, a compact 3x3 numeric keypad.

## 🛠 Features

- **3x3 Matrix**: Compact layout optimized for numeric input.
- **ZMK Studio Support**: Integrated support for [ZMK Studio](https://zmk.dev/docs/studio), allowing for real-time keymap adjustments without reflashing.
- **Bluetooth Connectivity**: Built for the `nice_nano_v2` controller.
- **Multi-Layer Support**:
  - **Default Layer**: Standard numeric keypad layout.
  - **BT Layer**: Bluetooth profile management and system controls (Bootloader, Studio unlock).

## 🚀 Hardware Specifications

- **Controller**: `nice_nano_v2`
- **Layout**: 3x3 Matrix (9 keys)
- **Diode Direction**: Column-to-Row

## ⌨️ Keymap Overview

### Default Layer
A standard numeric keypad setup for efficient data entry.

### Bluetooth & System Layer
Used for managing wireless connections and accessing firmware utilities:
- Bluetooth profile selection and clearing.
- Bootloader access.
- ZMK Studio unlock.

## 📦 Build and Installation

This project is configured to build via GitHub Actions. You can either use the default configuration or customize it for your own needs.

### Option 1: Use Default Firmware
If you don't need custom keymaps, you can download the pre-built firmware directly from this repository:
1. Go to the **Actions** tab at the top of this repository.
2. Select the latest successful workflow run (usually named "Build").
3. Scroll down to the **Artifacts** section.
4. Download the `firmware` artifact, extract the `.uf2` file, and flash it to your `nice_nano_v2`.

### Option 2: Customize and Build Your Own
If you want to change the keymap or settings:
1. Fork this repository to your own GitHub account.
2. Customize your `mb9i.keymap` file.
3. Commit and push your changes to trigger a new build.
4. Download your custom `.uf2` firmware from the **Actions** tab of *your* forked repository:
    - Select the latest successful workflow run.
    - Scroll down to the **Artifacts** section.
    - Download the `firmware` artifact and extract the `.uf2` file.
5. Flash the firmware to your `nice_nano_v2` controller.

## 📄 License

This project is licensed under the MIT License.
