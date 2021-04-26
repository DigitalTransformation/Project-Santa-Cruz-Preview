# How to update your Private Preview dev kit over a USB connection

### These instructions are explicitly for updating the private preview dev kits to the public preview software. If you have already updated your dev kit to the public preview build or if you purchased a public preview dev kit, please use [these instructions](https://docs.microsoft.com/en-us/azure/azure-percept/how-to-set-up-over-the-air-updates) for updating your dev kits. 

This guide will show you how to successfully update your dev kit's operating system and firmware over a USB connection.

> [!NOTE]
> Follow all instructions in order. Skipping steps could cause the update to fail and potentially put your dev kit in an unusable state.

## Prerequisites

- An Azure Percept DK
- A Windows, Linux, or OS X based host computer with Wi-Fi capability and an available USB-C or USB-A port
- A USB-C to USB-A cable (optional, sold separately)

## 1 - Download software tools and update files

1. [NXP UUU tool](https://github.com/NXPmicro/mfgtools/releases). Download the **Latest Release** uuu.exe file (for Windows) or the uuu file (for Linux) under the **Assets** tab.

1. [7-Zip](https://www.7-zip.org/). This software will be used for extracting the raw image file from its XZ compressed file. Download and install the appropriate .exe file.

1. [Download the update files](https://go.microsoft.com/fwlink/?linkid=2155734). This will automatically download a zipped package that contains all of the needed update files (fast-hab-fw.raw, Azure-Percept-DK-1.0.20210409.2055.raw, and emmc_full.txt).


## 2 - Set up your environment

1. Create a folder/directory on the host computer in a location that is easy to access via command line.

1. Copy the UUU tool (**uuu.exe** or **uuu**) to the new folder.

1. Extract the peviously downloaded zipped package so that all three of the update files are in the same folder as the UUU tool.

## 3 - Update your device

1. Connect to your dev kit [via SSH](./update-your-devkit-today/private-preview-update-instructions.md).

1. Next, open a Windows command prompt (**Start** > **cmd**) or a Linux terminal and navigate to the folder where the update files and UUU tool are stored. Enter the following command in the command prompt or terminal to prepare your computer to receive a flashable device:

    - Windows:

        ```console
        uuu -b emmc_full.txt fast-hab-fw.raw Azure-Percept-DK-1.0.20210409.2055.raw 
        ```

    - Linux:

        ```bash
        sudo ./uuu -b emmc_full.txt fast-hab-fw.raw Azure-Percept-DK-1.0.20210409.2055.raw
        ```

1. Disconnect the Azure Percept Vision device from the carrier board's USB-C port.

1. Connect the supplied USB-C cable to the carrier board's USB-C port and to the host computer's USB-C port. If your computer only has a USB-A port, connect a USB-C to USB-A cable (sold separately) to the carrier board and host computer.

1. In the SSH window, enter the following commands:

    1. Set the device to USB update mode:

        ```bash
        flagutil    -wBfRequestUsbFlash    -v1
        ```

    1. Reboot the device. The update installation will begin.

        ```bash
        reboot -f
        ```

1. Navigate back to the other command prompt or terminal. When the update is finished, you will see a message with ```Success 1    Failure 0```:

    > [!NOTE]
    > After updating, your device will be reset to factory settings and you will lose your Wi-Fi connection and SSH login.

1. Once the update is complete, power off the carrier board. Unplug the USB cable from the PC.
