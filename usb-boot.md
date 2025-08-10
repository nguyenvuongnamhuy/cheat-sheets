# Table of Contents

- [Create USB Boot](#create-usb-boot)
  - [Setup Ventoy](#setup-ventoy)
  - [Add OS versions](#add-os-versions)
- [Install OS](#install-os)
  - [Window](#window)
  - [Ubuntu](#ubuntu)

# Create USB Boot

- Use Ventoy to create usb multiboot

## Setup Ventoy

1. Must use an OS window to install Ventoy

- Download file `ventoy-x.x.x-windows.zip` from https://www.ventoy.net/en/download.html

2. Extract and run file Ventoy2Disk.exe
3. Select usb and click `Install` to install Ventoy into usb

## Add OS versions

1. Download OS any versions as `.iso` format (window 8, window 10, window 11, ubuntu 16, ubuntu 20, ...)
2. Copy paste file into usb

# Install OS

## Window

1. Plug the usb boot into the computer and start it up
2. Enter menu boot (usually press F2, F10, F12, Esc, Del, ...)
3. Prioritize usb boot first
4. Select save & exit
5. Wait for coming to Ventoy GUI
6. Select file .iso need to install
7. Follow the instructions
8. When it comes to select location to install Window, if can't select any disk, follow the below steps:

- Press `Shift + F10` or `Fn + Shift + F10` to open CMD
- Input:

  ```bash
    diskpart
    list disk
    select disk 0
    clean
    convert gpt
    exit
  ```

9. Then delete all parition (except VENTOY, VTOYEFI)
10. Start to shrink volume:

- Select `Disk 0`
- Click `Create partition` to create disk C, disk D, ...

11. Select disk C to install Window
12. Continue follow the instructions to install Window

- When it comes to select Wifi, press `Shift + F10` or `Fn + Shift + F10` to open CMD
  - Input `oobe\bypassnro` then press enter to by pass authentication
- Input `osk` then press enter if want to open the virtual keyboard (optional)
- Then repeat the steps as instructed
- When it comes to the step of selecting wifi again, click `I have no internet` and keep continue as instructions

13. After installation, the computer will be restarted
14. Select disk name for disk D:

- Press button `Window`
- Input `Disk management`
- Right click into Unallocated partition and click `Change Drive Letter and Paths`

## Ubuntu

// TODO

---
