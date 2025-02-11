# T480-OpenCore-Hackintosh

**Status: Maintained**

Supported OS's: Cataline, Big Sur, Monterey, Ventura, Sonoma

Highest supported OS: 14.2.1

Master doesnt have much, check the releases :D

Even if it shows a release released a while ago, please check the releases tab as i frequently upload pre releases which dont show up.

<img align="right" src="./Other/README_Resources/ThinkPad.gif" alt="T480 macOS" width="430">

[![OpenCore](https://img.shields.io/badge/OpenCore-0.7.3-blue.svg)](https://github.com/acidanthera/OpenCorePkg)
[![macOS-Previous](https://img.shields.io/badge/macOS-10.14.6-brown.svg)](https://github.com/EETagent/T480-OpenCore-Hackintosh/issues/11)
[![macOS-Stable](https://img.shields.io/badge/macOS-10.15.7-brightgreen.svg)](https://www.apple.com/macos/catalina/)
[![macOS-stable](https://img.shields.io/badge/macOS-11.6-blue.svg)](https://www.apple.com/macos/big-sur)
[![macOS-stable](https://img.shields.io/badge/macOS-12.4-purple.svg)](https://www.apple.com/macos/monterey)
[![macOS-stable](https://img.shields.io/badge/macOS-13.3.1-yellow.svg)](https://www.apple.com/macos/ventura)
[![macOS-stable](https://img.shields.io/badge/macOS-14.2.1-forest_green.svg)](https://www.apple.com/macos/sonoma)

**DISCLAIMER:**
Read the entire README and Dortania guides before you start. I am not responsible for any damage.
When you encounter bug or want to improve this repo, consider opening issue or pull request. 
If you find this bootloader configuration useful, consider giving it a star to make it more visible.

## Introduction

<details> 

<summary><strong>General knowledge & credits</strong></summary>

- To install macOS follow the guides provided by [Dortania](https://dortania.github.io/getting-started/)

- Useful tools by [CorpNewt](https://github.com/corpnewt) and [headkaze](https://github.com/headkaze/Hackintool)

- [CREDITS](CREDITS.md) file

</details>  

<details>

<summary><strong>Hardware</strong></summary>
<br>


[![UEFI](https://img.shields.io/badge/UEFI-N24ET61W-lightgrey)](https://pcsupport.lenovo.com/us/en/products/laptops-and-netbooks/thinkpad-t-series-laptops/thinkpad-t480-type-20l5-20l6/downloads/ds502355)
| Category  | Component                            | Note                                                                                                               |
| --------- | ------------------------------------ | ------------------------------------------------------------------------------------------------------------------ |
| CPU       | Intel Core i5-8350U                  | 20L50000MC                                                                                                         |
| GPU       | Intel UHD 620                        |                                                                                                                    |
| SSD       | Silicon Power P34A60 1TB NVMe        | Works perfectly with latest NVMeFix.kext                                                                           |
| Memory    | 16GB DDR4 2400Mhz                    |                                                                                                                    |
| Battery   | Dual battery                         |                                                                                                                    |
| Camera    | 720p Camera                          |                                                                                                                    |
| Wifi & BT | BCM93452Z                            | Use AirportItlwm for your macOS version and enjoy native Wi-Fi control, or use Heliport app. Broadcom is native.   |                     
| Input     | PS2 Keyboard & Synaptics TrackPad    | [YogaSMC](https://github.com/zhen-zen/YogaSMC) for media keys like microphone switch, etc. PrtSc is mapped as F13. |

</details>  

<details>

<summary><strong>Main software</strong></summary>
<br>

| Component      | Version        |
| -------------- | -------------- |
| OpenCore       | v0.9.4         |
| macOS Catalina | 10.15.7 (19H2) |
| macOS Big Sur  | 11.2.2 (20D80) |
| macOS Monterey | 12.6.1 (21G217)|
| macOS Ventura  | 13.5.1 (22G90) |
| MacOS Sonoma   | 14.2.1 (23C71) |

</details>

<details>

<summary><strong>Kernel extensions</strong></summary>
<br>

| Kext                   | Comment        
|:---------------------- | ------------------------------
| AirportItlwm           | Latest(Intel cards only)         
| AppleALC               | Latest Speaker drivers
| BrightnessKeys         | Latest         
| CPUFriend              | Latest CPU power management
| CPUFriendDataProvider  | Latest i5-8350U
| HibernationFixup       | Latest         
| HoRNDIS                | Disabled, 9.2  
| IntelBluetoothFirmware | Latest (Intel cards only)          
| IntelBluetoothInjector | Latest (Intel cards only)         
| IntelMausi             | Latest Ethernet controller
| Lilu                   | Latest         
| NoTouchID              | Latest         
| NVMeFix                | Latest NVMe SSD fix
| RTCMemoryFixup         | Latest Real time clock fix
| VirtualSMC             | Latest         
| VoltageShift           | Disabled, 1.22 
| VoodooPS2Controller    | Latest         
| VoodooRMI              | Latest         
| VoodooI2C              | Latest Touchscreen drivers
| VooDooI2CHID           | Latest Intel satellite kext
| VoodooSMBus            | Latest         
| WhateverGreen          | Latest         
| YogaSMC                | Latest Lenovo SMC

</details>
<details>

<summary><strong>UEFI drivers</strong></summary>
<br>

| Driver          | Version           |
|:---------------:| ----------------- |
| AudioDxe.efi    | OpenCorePkg 0.9.8 |
| HfsPlus.efi     | OcBinaryData      |
| OpenCanopy.efi  | OpenCorePkg 0.9.8 |
| OpenRuntime.efi | OpenCorePkg 0.9.8 |
</details>

<details>
    <summary><strong>Neofetch screenshots</strong></summary>
    <br>
    <p float="left">
        <img src="./Other/README_Resources/Neofetch-Catalina.png" alt="Neofetch Catalina" width="350">
        <img src="./Other/README_Resources/Neofetch-BigSur.png" alt="Neofetch Catalina" width="350">
    </p>
</details> 

## Before installation

<details>  

<summary><strong>UEFI settings</strong></summary>
<br>

**Security**

- `Security Chip` **Disabled**
- `Memory Protection -> Execution Prevention` **Enabled**
- `Virtualization -> Intel Virtualization Technology` **Enabled**
- `Virtualization -> Intel VT-d Feature` **Enabled**
- `Anti-Theft -> Computrace -> Current Setting` **Disabled**
- `Secure Boot -> Secure Boot` **Disabled**
- `Intel SGX -> Intel SGX Control` **Disabled**
- `I/O Port Access -> Thunderbolt` **Disabled**
- `Device Guard` **Disabled**

**Startup**

- `UEFI/Legacy Boot` **UEFI Only**
- `CSM Support` **No**

**Thunderbolt**

- `Thunderbolt BIOS Assist Mode` **Disabled**
- `Wake by Thunderbolt(TM) 3` **Enabled**
- `Security Level` **User Authorization**
- `Support in Pre Boot Environment -> Thunderbolt(TM) device` **Enabled**

</details>  

<details>

<summary><strong>Own prev-lang-kbd</strong></summary>
<br>

Either add as a string or as a data ( HEX data [(ProperTree)](https://github.com/corpnewt/ProperTree) )

Format is lang-COUNTRY:keyboard

- 🇺🇸 | [0] en_US - U.S --> en-US:0 --> 656e2d55 533a30

- 🇨🇿 | [30776] cs - Czech --> cs-CZ:30776 --> 63732d43 5a3a3330 373736

- 🇨🇿 | cs-CZ:0 --> 63732d43 5a3a30

etc.

[AppleKeyboardLayouts.txt](https://github.com/acidanthera/OpenCorePkg/blob/master/Utilities/AppleKeyboardLayouts/AppleKeyboardLayouts.txt)

</details>

<details>

<summary><strong>Secure Boot (Optional)</strong></summary>
<br>

1. Set Secure Boot to Setup Mode. Secure Boot should be reported as off by UEFI main tab
2. Create FAT32 formatted USB
3. Create EFI folder in the root of the newly formatted flash drive and move there content of SecureBoot/KeyTool
4. Boot flash drive via F12 boot menu
5. Choose **Edit keys**


<img src="./Other/README_Resources/SecureBoot/MainMenu.png" alt="Main menu">

6. Start by **replacing** Signature Database. Select .auth file


<img src="./Other/README_Resources/SecureBoot/ManipulateKey.png" alt="Select key to manipulate with">
<img src="./Other/README_Resources/SecureBoot/SelectAuth.png" alt="Select .auth file">


7. Do the same for Key Exchange Keys Database (KEK) and Platform Key (PK) **in this order**
8. Exit and shutdown your machine
9. Boot into the UEFI settings and check if Secure Boot is reported as `on`
10. Boot you favorite OS with Secure Boot enabled

[More detailed information here](https://habr.com/en/post/273497)

```diff
! Still quite experimental
```

</details>

## Post-Install

<details>  

<summary><strong>Colour banding</strong></summary>
<br>

If you encounter some serious colour banding issues ( Keep in mind that T480 1080p stock panel colour accuracy is not really good, cca 50-60% sRGB), your only solution is to replace GPU properties as bellow or replace the stock panel with one from T490 (400 nits, Low power).

```
<key>AAPL,ig-platform-id</key>
<data>AAAWGQ==</data>
<key>device-id</key>
<data>FhkAAA==</data>
</dict>
```

Do not use these any additional boot arguments! Get custom WhateverGreen version instead from Other folder

You can check your screen in gradient test [here](https://www.eizo.be/monitor-test/) or just by simple look at Launchpad background.

</details>  

<details>  

<summary><strong>Generate your own SMBIOS</strong></summary>
<br>

[GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)

- MacBookPro14,1

- MacBookPro15,2

</details>  

<details>  

<summary><strong>CPUFriend power management</strong></summary>
<br>

Generate CPUFriendDataProvider for your machine [here](https://github.com/fewtarius/CPUFriendFriend) or use at your own risk files provided in the Other folder.

</details>  

<details>  

<summary><strong>VoltageShift undervolt</strong></summary>
<br>

It is possible to use VoltageShift directly from the EFI folder instead of disabling SIP. You need to use specific version provided in the Other folder.

```diff
! If you want to use this feature, enable it in config.plist
```
</details>  

<details>  

<summary><strong>Android USB Tethering | HoRNDIS</strong></summary>
<br>

> **Important:** Mac computers can't tether with Android. 

I don't think so Google.

1. Using a USB cable, connect your phone to the other device. A "Connected as a…" notification shows at the top of the screen.
2. Open your phone's Settings app.
3. Tap Network & internet ![And then](https://lh3.googleusercontent.com/WD3LKKej34vq3cZXwilgeahIPOiokN2uarmkDxtMqKMFg4SSys8BkOBJbn4_4R930gE=h18 "And then") Hotspot & tethering.
4. Turn on USB tethering.

You should see new Ethernet connection in the network settings. Works with USB Type C and USB A.

```diff
! If you want to use this feature, enable it in config.plist
```
Problems with recreating new `en` device every time are now solved on latest macOS versions with patched version of this kext. If it does not work for you, revert to official version.

</details>  

## Status

<details>  

<summary><strong>What's working ✅</strong></summary>

- [x] Battery percentage

- [x] Bluetooth - Intel Wireless-AC 8265 (0x0A2B) (Not maintained in repo)

- [X] Broadcom Bluetooth - All works! (native) 

- [x] Boot chime

- [x] Boot menu `OpenCanopy` 

- [x] CPU power management / performance `Now on par with Windows without XTU undervolt.`

- [x] FireVault 2 `No config.plist changes needed` 

- [x] GPU UHD 620 hardware acceleration / performance 

- [x] HDMI `Closed lid. With audio.`

- [x] iMessage, FaceTime, App Store, iTunes Store. **Generate your own SMBIOS**

- [x] Intel I219V Ethernet port `Full 1 Gbps speeds and external eithernet adapter next to TB port also works`

- [x] Keyboard `Volume and brightness hotkeys. Another media keys with YogaSMC.`

- [x] Microphone `With keyboard switch using YogaSMC.`

- [x] Realtek® ALC3287 ("ALC257") Audio

- [x] SD card reader `Fortunately, USB connected.`

- [x] Sidecar wired `Works with 15,2 SMBIOS. Wireless with Broadcom Card`

- [x] Sleep/Wake `Hibernatemode 25 for the best results. `

- [ ] Thunderbolt  `40 Gbps after start and 10 Gbps after sleep wake`

- [x] TouchPad `1-5 fingers swipe works. Emulate force touch using longer and more voluminous touch.`

- [x] TrackPoint  `Works perfectly. Just like on Windows or Linux.`

- [x] USB Ports `USB Map is different for devices with Windows Hello camera.`

- [x] Web camera `Works well with MacOS with no bugs`

- [x] Wifi - Intel Wireless-AC 8265 `works using heliport and itlwm with big sur`

- [X] Broadcom Wifi - Native broadcom cards work perfectly with all features available wirelessly too. Legacy 

- [x] DRM `Widevine, validated on Firefox 82. WhateverGreen's DRM is broken on Big Sur`

</details>  

<details>  

<summary><strong>What's not working ⚠️</strong></summary>
    
- [ ] Intel WIFI  `Most of it works but MIGHT still be buggy (Not Maintained in this repo). If any bugs, check the dortainia guides regarding intel wifi. `(Broadcom native is stable)

- [ ] Fingerprint reader  `There is finally after many years working driver for Linux (python-validity), don't expect macOS driver any time soon.` (Able to see it as a synaptics usb device and can be used on an ubuntu vm on macos)

- [ ] Continuity(Intel Cards) `If you want to use this feature, buy a compatible Broadcom card!`(Latest release only has drivers for Broadcom cards)


</details>  

<summary><strong>Post-Install</strong></summary>
This part has been copied from Tienhyun5312

Audio jack

If you have audio glitchy after plug your headphone jack, use this.

Go to releases and find fixes release.
Go into alc_fix folder, run install.sh and reboot.

***Issue Fixed on Ventura and above***

</details>

## UEFI modding

<details>  

<summary><strong>CFG Lock | Advanced menu</strong></summary>
<br>

<img align="left" src="./Other/README_Resources/SPI_Programmer_CH341a.jpg" alt="SPI_Programmer_CH341a.jpg" width="220">

It's possible to unlock Advanced menu thus disable CFG Lock natively in UEFI + Other Advanced menu benefits. SPI Programmer CH341a is required

<br>
https://www.reddit.com/r/thinkpad/comments/ffqqx5/currently_testing_skyra1n/

[T480 consuming 60w (~85w total) - unlimited TDP : thinkpad](https://www.reddit.com/r/thinkpad/comments/g8fk51/t480_consuming_60w_85w_total_unlimited_tdp/)

[ThinkPad discord](discord.gg/Ybdz7AS)

</details>  
