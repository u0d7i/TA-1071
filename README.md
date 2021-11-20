# TA-1071
TA-1071 Nokia 8110 4G Single-SIM Europe

## Under the cover
CODE: 23ARG05ROW1<br>
IMEI: 3544760900XXXXX<br>
HMD Global Oy<br>
Model: TA-1071<br>
MADE IN VIETNAM<br>
FCC ID: 2A_JOTTA-1071<br>

## Battery
BV-6A 1500mAh 3.85V 5.78Wh

## GUI
Settings -> Device -> Device Information:<br>
Model: Nokia 8110 4G<br>
Software: 11.00.17.03

More Information:<br>
OS Version: 2.5<br>
Hardware Revision: qcom<br>
Platform Version: 48.0a2

```*#0000#``` displays:<br>
Nokia 8110 4G<br>
11.00.17.03<br>
18-06-05<br>
TA-1071<br>
(c)Nokia<br>
Variant:23ARG05ROW1/SS<br>

## Dmesg
(timestamps removed, serial nr altered)<br>
In normal mode:
```
usb 1-8: new high-speed USB device number 6 using xhci_hcd
usb 1-8: New USB device found, idVendor=05c6, idProduct=9092, bcdDevice= 3.10
usb 1-8: New USB device strings: Mfr=1, Product=2, SerialNumber=3
usb 1-8: Product: Android
usb 1-8: Manufacturer: Android
usb 1-8: SerialNumber: a012345b
```
In debug mode (after entering ```*#*#33284#*#*``` and "bug" icon appears):
```
usb 1-8: new high-speed USB device number 7 using xhci_hcd
usb 1-8: New USB device found, idVendor=05c6, idProduct=9091, bcdDevice= 3.10
usb 1-8: New USB device strings: Mfr=1, Product=2, SerialNumber=3
usb 1-8: Product: Android
usb 1-8: Manufacturer: Android
usb 1-8: SerialNumber: a012345b
```

## ADB
Enable ADB access:<br>
Dial the code ```*#*#33284#*#*```<br>
A bug icon should appear in the taskbar, 'adb devices' shows device as serial nr. present.

```
$ adb shell
shell@Nokia 8110 4G:/ $ uname -a
Linux localhost 3.10.49-ged30a3a-00708-ge9a40b3 #1 SMP PREEMPT Tue Jun 5 17:56:08 CST 2018 armv7l
```

# Recovery
Power-off, hold arrow-up while powering on.

or via adb: ```adb reboot recovery```
