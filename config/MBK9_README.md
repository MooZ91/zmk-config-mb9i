# MBK9 3x3 ZMK Keyboard Configuration

A complete ZMK firmware configuration for a 3x3 mechanical keyboard with Bluetooth, RGB underglow, and VIA compatibility.

## Features

✅ **3x3 Key Matrix** - 9-key layout perfect for macro pads or portable keyboards  
✅ **Bluetooth Support** - Wireless connectivity with nRF52840  
✅ **RGB Underglow** - WS2812B addressable LED support  
✅ **VIA Compatible** - Configure keys without reflashing  
✅ **Multi-Layer** - 4 programmable layers with easy switching  
✅ **Combo Keys** - Use key combinations for shortcuts  

## Hardware Requirements

- **MCU**: nRF52840 (Nordic Semiconductor)
- **Matrix**: 3 columns × 3 rows (9 keys total)
- **LEDs**: WS2812B/NeoPixel RGB (9 units recommended for one per key)
- **Power**: USB-C or battery with wireless charging support

## GPIO Pin Configuration

### Matrix Pins
| Component | Pins |
|-----------|------|
| Columns (3) | GPIO 4, 5, 6 |
| Rows (3) | GPIO 7, 8, 9 |
| RGB LED Data | GPIO 10 |
| Status LED | GPIO 11 |

### Optional Pins
- **UART RX**: GPIO 8
- **UART TX**: GPIO 6
- **SPI SCK**: GPIO 19
- **SPI MOSI**: GPIO 20
- **I2C SDA**: GPIO 23
- **I2C SCL**: GPIO 24

**Note**: These pin assignments can be modified in:
- `mbk9.dts` for the matrix and LEDs
- `mbk9-pinctrl.dtsi` for peripheral interfaces

## Keymap Layers

### Layer 0: Base Layer
Standard numpad layout (1-9)

```
1  2  3
4  5  6
7  8  9
```

### Layer 1: RGB/Bluetooth Control
- Top row: RGB on/off/toggle
- Middle row: Bluetooth device selection 0, 1, and clear
- Bottom row: RGB hue and saturation controls

### Layer 2: Function Keys
F1-F9 function keys

### Layer 3: Media Controls
- Volume up/down/mute
- Play/pause, previous, next track
- Print screen and pause break

## Layer Activation

Layers can be activated via combo keys:
- **Top row press** (1+2+3) → RGB/BT layer
- **Middle row press** (4+5+6) → Function keys layer
- **Bottom row press** (7+8+9) → Media/Special layer

## Configuration Files

### Main Files
1. **config/mbk9.keymap** - Keymap definitions (layers, key bindings)
2. **boards/mooz/mbk9/mbk9.dts** - Hardware configuration
3. **boards/mooz/mbk9/mbk9-pinctrl.dtsi** - Pin definitions
4. **boards/mooz/mbk9/mbk9-layouts.dtsi** - Physical key layout
5. **boards/mooz/mbk9/mbk9.conf** - Build configuration

## Building

```bash
west build -b mooz_mbk9 -d build/mooz_mbk9 -- -DZMK_CONFIG="$(pwd)/config"
```

## Flashing

After build completes:

```bash
west flash -d build/mooz_mbk9
```

## Customization

### Change Key Bindings
Edit the keymaps in [config/mbk9.keymap](config/mbk9.keymap):

```c
default_layer {
    bindings = <
        &kp A &kp B &kp C
        // ... more keys
    >;
};
```

### Modify RGB Settings
In [boards/mooz/mbk9/mbk9.conf](boards/mooz/mbk9/mbk9.conf):

```conf
CONFIG_ZMK_RGB_UNDERGLOW_HUE_START=120  # Start at green
CONFIG_ZMK_RGB_UNDERGLOW_BRT_START=50   # 50% brightness
```

### Add/Remove Layers
Add new layer definitions in the keymap file:

```c
my_custom_layer {
    display-name = "Custom";
    bindings = <
        &kp ... &kp ... &kp ...
        // ...
    >;
};
```

### Adjust GPIO Pins
For your specific hardware, modify pin assignments in [boards/mooz/mbk9/mbk9.dts](boards/mooz/mbk9/mbk9.dts):

```c
col-gpios
    = <&gpio0 YOUR_PIN_A GPIO_ACTIVE_HIGH>
    , <&gpio0 YOUR_PIN_B GPIO_ACTIVE_HIGH>
    , <&gpio0 YOUR_PIN_C GPIO_ACTIVE_HIGH>
    ;
```

## VIA Support

VIA compatibility is built into the firmware. To use VIA:

1. Install [VIA app](https://www.caniusevia.com/)
2. Connect your keyboard
3. Create or load a VIA JSON definition for your 3x3 layout
4. Remap keys in real-time without reflashing

## Bluetooth Usage

### Pairing
- Use the BT layer (press 1+2+3)
- Press `BT_SEL 0` or `BT_SEL 1` to switch between paired devices
- Hold shift and press a BT key for additional options

### Clear All Bonds
Press the `BT_CLR` key in the RGB/BT layer to clear all paired devices

## RGB Control

When in the RGB/BT layer:
- **Hue Up/Down**: Adjust color
- **Saturation Up**: Increase vividness
- **RGB On**: Enable underglow
- **RGB Off**: Disable underglow
- **RGB Toggle**: Quick on/off

## Power Management

- **Idle timeout**: 30 seconds
- **Sleep mode**: Enabled for battery savings
- Wireless broadcast stops during sleep
- Wake by pressing any key

## Advanced Customization

### Add Macros
```c
macros {
    my_macro: my_macro {
        compatible = "zmk,behavior-macro";
        #binding-cells = <0>;
        bindings = <&kp H &kp E &kp L &kp L &kp O>;
    };
};
```

### Add More Combos
```c
combos {
    combo_example {
        timeout-ms = <50>;
        key-positions = <0 1>;  // Keys at position 0 and 1
        bindings = <&mo 1>;     // Activate layer 1
    };
};
```

### Enable Display
Uncomment in [mbk9.conf](boards/mooz/mbk9/mbk9.conf):
```conf
CONFIG_ZMK_DISPLAY=y
CONFIG_SSD1306=y
CONFIG_I2C=y
```

## Troubleshooting

### Keys not responding
- Check GPIO pin assignments match your PCB
- Verify diode direction matches `diode-direction` setting
- Test with USB connection to see debug output

### RGB not working
- Ensure `WS2812B_STRIP=y` is enabled in config
- Check RGB data pin is correctly connected
- Verify LED chain length matches actual LED count

### Bluetooth not connecting
- Clear all bonds: Hold and press `BT_CLR`
- Try pairing with specific device using `BT_SEL`
- Check nRF52840 power supply is stable

### Build fails
- Ensure ZMK repository is up to date: `west update`
- Clean build: `rm -rf build zephyr-venv`
- Check Python version is 3.8 or higher

## Resources

- [ZMK Documentation](https://zmk.dev/)
- [ZMK Discord Community](https://discord.gg/8J52v8K)
- [VIA Documentation](https://www.caniusevia.com/)
- [nRF52840 Datasheet](https://www.nordicsemi.com/products/nrf52840)

## License

This configuration is provided as-is for personal use. Refer to ZMK's MIT license for the firmware itself.

---

**Last Updated**: March 30, 2026  
**Maintainer**: MBK9 Project
