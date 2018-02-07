% Use STM32 Bluepill with Lora on Arduino

---

**TLDR:**
 * Install Arduino IDE
 * Use `https://raw.githubusercontent.com/stm32duino/BoardManagerFiles/d1c46284dec37305d563a87eecfb545e3c66a166/STM32/package_stm_index.json` for the Boardmanager preferences
 * Add Bluepill from Boardmanager


---

**I assume you are using a BluePill Board with an STLink programmer. You can burn the STM32duino bootloader, which will enable you to program over USB. This is not in the scope of this HowTo (for now).**

## Download the Arduino IDE

Go to the [Arduino Download Page](https://www.arduino.cc/en/Main/Software) and Download the Package that coresponds to your Operating System.

* On Linux you can untar the archive with `tar xfv Downloads/arduino-*-linux64.tar.xz`
* On Windows you can run the installer or use the explorer to unzip the downloaded archive.

Now start the Arduino IDE by running the `arduino` binary.

## Add STM32 Boardsupport

Go to File -> Preferences and copy the following URL to the `Additional Board Manager URLs` field:
`https://raw.githubusercontent.com/stm32duino/BoardManagerFiles/d1c46284dec37305d563a87eecfb545e3c66a166/STM32/package_stm_index.json`

[![](0x03/preferences_scaled.jpg "preferences")](0x03/preferences.png)

For now the STM32duino project is refactoring its codebase and does not support the Bluepill. We use an old snapshot to circumvate this. Once this is fixed we can use this URL: `https://github.com/stm32duino/BoardManagerFiles/raw/master/STM32/package_stm_index.json`

### Driver (Windows only)
On **Windows** you will have to download the [driver](http://www.st.com/content/st_com/en/products/development-tools/software-development-tools/stm32-software-development-tools/stm32-utilities/stsw-link009.html) and if you want the [device manager utility](http://www.st.com/content/st_com/en/products/development-tools/software-development-tools/stm32-software-development-tools/stm32-programmers/stsw-link004.html), which will both *require* you to have a free account.

## Test Blink Example

Choose Tools->Board->Boardmanager... , search for `bluepill` and install the `STM32F1xx Cores by ST-Microelectronics` package.

Go to File->Examples->01. Basics->Blink

Now go to Tools->Board->STM32F1xx->BluePill F103C8.
Choose Tools->Upload Method->STLink

Click Upload. You should end up with an blinking LED.

### Troubleshooting:
 * "STLink not found":
     * On Windows reinstall the driver. It will tell you, if a STLink was found and configured during installation
     * On Linux unplug the STLink and use `dmesg --follow` to ensure it is detected correctly
 * "*Board not found*" or "*Device not found*"
     * Ensure that both Boot Jumpers are set to 0.
     * Verify the electric connections between STLink and BluePill
     * Replug STLink
     * Try flashing with the BOOT0 jumper set to 1

## Talking to Lora module
For now there is currently no compatible `Lora MAC in C` short `lmic` port. I will update this document once it get it to work.
