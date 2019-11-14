# Firmware for M5StickC which allows bluetooth connection to xdrip for iOS
##### M5Stick c xdrip monitor<br/>Copyright (C) Johan Degraeve 

This is a modified version of https://github.com/JohanDegraeve/M5_NightscoutMon

### What is available in this project

There's only one screen, with the bloodglucose value and an arrow. Always the same color. A bluetooth connection can be made with an iOS device that has xdrip installed : https://github.com/JohanDegraeve/xdripswift. The iOS device can send readings directly to the M5Stick

With xdrip one can
 * Scan for and connect to multiple M5Stacks.
 * configure the text color
 * configure the background color
 * rotate the screen
 * configure (optional) a password ==> if a password is set in the M5Stack, then the same password must be configured in the xdrip app - this is not strictly necessary, see further on
 * the selected bloodglucose unit (mgdl or mmol) will also be sent to the M5Stack
 * Send readings : the M5Stack can receive readings from xdrip.

### To compile

To compile, in Arduino IDE set Tools - Partition Scheme - No OTA (Large APP). This is because the BLE library needs a lot of memory

### Installaton and Support

Download latest M5Burner release : https://github.com/JohanDegraeve/M5_NightscoutMon/releases
It is Windows executable with binary M5Stack firmware included. Just unzip it, start the M5Burner.exe, choose COM port where your M5Stack is connected and burn the firmware.

More info ? send an email to xdrip@proximus.be

### microSD card

The M5Stack can work without microSD card and without the M5NS.INI file. If the file is missing, then whenever the M5Stack restarts, xdrip will need to be connected to configure the required parameters

### authentication - passwords

There's no strong security implemented. Just to avoid that someone else (my neighbour) connects to my M5Stack and starts sending readings, there's some authentication: xDrip (on iOS device) needs to authenticate itself towards the M5Stack.
There's two options :
* a fixed password : in this case a micro SD card must be used in the M5Stack, the ini file must have a password must be stored in the variable blepassword. Each iOS device that has xdrip installed (usually there's only one but you may have more), must have the same password configured in the Settings (see Settings - M5Stack)
* a random password : if there's no parameter named blepassword configured in the ini file, then at each startup, and the first time it connects to xDrip, it will generate a random password and send this to xdrip. You can see it in the M5Stack settings. If every there's a disconnect and a reconnect, the xdrip app must authenticate with this password


