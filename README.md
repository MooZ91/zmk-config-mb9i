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

This project is configured to build via GitHub Actions.

1. Fork this repository to your own GitHub account.
2. Customize your `mb9i.keymap` file.
3. Commit and push your changes.
4. Download the resulting `.uf2` firmware artifact from the GitHub Actions tab.
5. Flash the firmware to your `nice_nano_v2` controller.

## 📄 License

This project is licensed under the MIT License.
