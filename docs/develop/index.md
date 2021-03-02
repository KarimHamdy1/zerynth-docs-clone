---
title: asdasdasdasdasdasdascxzczxczxczx
---
# lets do a demooooooooooooooooozxczxczxczx

![](https://docs.zerynth.com/latest/develop/img/Create%20a%20Zerynth%20User%20Account.png)

Note

If you choose manual credentials you will need to verify your new account by clicking the link provided in the confirmation email

Warning

The first time you create a user account or if you have sign-in issues, a restart of Zerynth Studio might be necessary

### Prepare a device[](https://docs.zerynth.com/latest/develop/#prepare-a-device "Permanent link")

To make a device usable with Zerynth, you need to **Connect** it and install **Zerynth OS** on it.

According to the platform used and to the connected device, you may need to install the related drivers for enabling it in the development machine.

Warning

Procedure to install drivers, if needed, is reported device by device in [Supported Devices](https://docs.zerynth.com/latest/reference/boards/).

To install Zerynth OS, you can click the **Z** button and install it in one click.

If you want more fine grained control on the features of the Zerynth OS, keep on reading.

The **Registration** phase is the process of retrieving the device info to allow the Zerynth backend to know about the device.

![](https://docs.zerynth.com/latest/develop/img/Registration%20phase.png)

If the device has never been connected before, by clicking the “Z” button, the registration dialog, shown above, is displayed.

To register a new device, you can follow these steps:

1. connect your device to the machine. The “Devices Management Widget” notifies the devices list update with a yellow blink;
2. select the device from the dropdown menu;
3. click on the “Z” button. Zerynth Studio will guide you in the entire process through info messages displayed in the log console section at the bottom of the screen.

Note

“Powered by Zerynth” devices are accompained by a redeemable code that can be inserted in the above window and exchanged for a free virtual machine license.

Warning

Some devices require to be set in Device Firmware Update (DFU) mode in order to allow their registration and the flashing of the Zerynth Virtual Machine. Detailed guides on how to put them in DFU mode is available in the [Supported Devices](https://docs.zerynth.com/latest/reference/boards/) section of the documentation.

Once registration has been performed, you are given the option to create a Virtual Machine for the registered device by clicking again the “Z” button.

![](https://docs.zerynth.com/latest/develop/img/create%20a%20Virtual%20Machine.png)

Note

A device can always be registered again with the dedicated dialog button.

In the figure below, after clicking the “Create” button, the user can select one available of different virtual machines compatible with the target device choosing the licenses (Starter/Premium), the real time operating system from those supported for the target device, and (for Premium licenses only) the features to be included in the virtual machine (FOTA, Power Saving, Secure Firmware, etc.).