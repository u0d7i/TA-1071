# TA-1071
TA-1071 Nokia 8110 4G Single-SIM Europe

![TA-1071 Nokia 8110 4G Single-SIM Europe](img/nokia-8110-4g-single-sim-ta-1071.jpg?raw=true "TA-1071 Nokia 8110 4G Single-SIM Europe")

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
In edl mode (after 'adb reboot edl', remove the battery to exit edl mode):
```
usb 1-8: new high-speed USB device number 32 using xhci_hcd
usb 1-8: New USB device found, idVendor=05c6, idProduct=9008, bcdDevice= 0.00
usb 1-8: New USB device strings: Mfr=1, Product=2, SerialNumber=0
usb 1-8: Product: QHSUSB__BULK
usb 1-8: Manufacturer: Qualcomm CDMA Technologies MSM
usbcore: registered new interface driver qcserial
usbserial: USB Serial support registered for Qualcomm USB modem
qcserial 1-8:1.0: Qualcomm USB modem converter detected
usb 1-8: Qualcomm USB modem converter now attached to ttyUSB0
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

## Recovery
Power-off, hold arrow-up while powering on.

or via adb: ```adb reboot recovery```

## Root

```
$ adb push /tmp/adbroot /data/local/tmp
$ adb shell
shell@Nokia 8110 4G:/ $ cd /data/local/tmp
shell@Nokia 8110 4G:/data/local/tmp $ chmod +x adbroot
shell@Nokia 8110 4G:/data/local/tmp $ ./adbroot
--------------------------------------------------------------------
--- KaiOS adb-root script by speedUpLoop                         ---
--- heavily inspired by root method of GerdaOS / Project Pris    ---
--- by Luxferre / Nihilist                                       ---
--------------------------------------------------------------------

please open following url in phone's browser
---------------------------------------------> http://localhost:8080
and click the button...
done!

--------------------------------------------------------------------
if no error message was shown in browser after clicking the button,
you now have adb-root -- this works until reboot
--------------------------------------------------------------------
```

Root stays untill reboot, do a factory reset to repeat.

## Backup
Make sure you are root, you have SD card insterted (upper slot, vfat formatted (exfat formatted sd card was not recognised).
```
root@Nokia 8110 4G:/ # for P in $(ls /dev/block/bootdevice/by-name/); do echo "dumping $P"; dd if=/dev/block/bootdevice/by-name/$P of=/sdcard/backup/$(basename $P).img bs=2048; done
root@Nokia 8110 4G:/ # getprop > /sdcard/backup/getprop.txt
```

## OTA Update

```
root@Nokia 8110 4G:/ # ls -al /data/fota/downloaded/
-rw------- root     root     39233538 2021-11-24 10:54 update.zip

root@Nokia 8110 4G:/ # md5sum /data/fota/downloaded/update.zip                 
6689c479fff18e7f61d3e98d1efcbe72  /data/fota/downloaded/update.zip

root@Nokia 8110 4G:/ # mkdir /sdcard/update
root@Nokia 8110 4G:/ # cp /data/fota/downloaded/update.zip /sdcard/update/
```

## Links

* https://en.wikipedia.org/wiki/Nokia_8110_4G
* https://gerda.tech/
* https://wiki.bananahackers.net/
* https://ivan-hc.github.io/bananahackers/
* https://github.com/andybalholm/edl
* https://edl.bananahackers.net/
* https://groups.google.com/g/bananahackers
* https://4pda.to/forum/index.php?showtopic=890710 (ru)
* https://4pda.to/forum/index.php?showtopic=950670 (ru)
* https://4pda.to/forum/index.php?showtopic=975097 (ru)

### EDL research
* https://github.com/bkerler/edl/
* https://bkerler.github.io/2020/08/03/bring-light-to-the-darkness-p3/
* https://github.com/Zalexanninev15/emmcdl
* https://github.com/Zalexanninev15/PFT-Linux
* https://anantamaha.com/how-to-backup-firmware-from-qualcomm-android-using-qfil/
* https://wiki.bananahackers.net/development/edl
* https://github.com/andybalholm/edl
