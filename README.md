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

## Stock Root

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

## ADB Backup
Make sure you are root, you have SD card insterted (upper slot, vfat formatted, exfat formatted sd card was not recognised).
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

After the OTA update the latest firmware version for this model is 17.00.17.01 .

Also, usb product ID changes in dmesg:

```
usb 1-8: new high-speed USB device number 24 using xhci_hcd
usb 1-8: New USB device found, idVendor=05c6, idProduct=900e, bcdDevice= 3.10
usb 1-8: New USB device strings: Mfr=1, Product=2, SerialNumber=3
usb 1-8: Product: Android
usb 1-8: Manufacturer: Android
usb 1-8: SerialNumber: a012345b
usb 1-8: USB disconnect, device number 24
usb 1-8: new high-speed USB device number 25 using xhci_hcd
usb 1-8: New USB device found, idVendor=05c6, idProduct=f003, bcdDevice= 3.10
usb 1-8: New USB device strings: Mfr=1, Product=2, SerialNumber=3
usb 1-8: Product: Android
usb 1-8: Manufacturer: Android
usb 1-8: SerialNumber: a012345b

```

After doing "Settings -> Storage -> USB Storage -> Disabled":

```
usb 1-8: USB disconnect, device number 25
usb 1-8: new high-speed USB device number 26 using xhci_hcd
usb 1-8: New USB device found, idVendor=05c6, idProduct=900e, bcdDevice= 3.10
usb 1-8: New USB device strings: Mfr=1, Product=2, SerialNumber=3
usb 1-8: Product: Android
usb 1-8: Manufacturer: Android
usb 1-8: SerialNumber: a012345b
```

## EDL
Enter [EDL](https://en.wikipedia.org/wiki/Qualcomm_EDL_mode) mode by:
* from powered off device hold Up + Down and instert USB cable or hold power-on, (screen blinks and goes blank)
* from adb: 'adb reboot edl'

The [knowlingly working edl tool](https://github.com/andybalholm/edl) requires Python 3.7,
but at the time of writting default Debian Python version is 3.9.
We'll be using [pyenv](https://github.com/pyenv/pyenv) to install 3.7.

Prepare the env:

```
$ curl https://pyenv.run | bash
$ export PATH="$HOME/.pyenv/bin:$PATH"
$ eval "$(pyenv init --path)"
$ eval "$(pyenv virtualenv-init -)"

$ pyenv versions
$ pyenv install 3.7.12
$ pyenv global 3.7.12
$ pip3.7 install pyusb pyserial capstone keystone-engine

$ git clone https://github.com/andybalholm/edl
$ cd edl/
$ sudo cp 51-edl.rules /etc/udev/rules.d/
$ sudo cp 50-android.rules /etc/udev/rules.d/
$ sudo udevadm control -R
$ echo "blacklist qcserial" | sudo tee -a /etc/modprobe.d/blacklist.conf
$ wget -c https://edl.bananahackers.net/loaders/8110.mbn
```

Test if edl tool is working:

```
$ python3.7 edl.py -loader 8110.mbn  -reset

Qualcomm Sahara / Firehose Client (c) B.Kerler 2018-2019.


Using loader 8110.mbn ...
Waiting for the device
........Device detected :)
Mode detected: Sahara

------------------------
HWID:              0x000940e100420050 (MSM_ID:0x000940e1,OEM_ID:0x0042,MODEL_ID:0x0050)
PK_HASH:           0x1357fdaeabb7becbe49095f000d9d3dadf198885106d98598cac6d1b9b2edb3a
Serial:            0xa012345b
SBL Version:       0x00000000

Successfully uploaded programmer :)
TargetName=MSM8909
MemoryName=eMMC
Version=1
Reset succeeded.

```

NOTE: Unfortunately, you must restart the phone after each edl command except reset, because an attempt to execute edl command second time fails with ``Mode detected: Unknown``, despite phone still appearing in edl mode:

```
Using loader 8110.mbn ...
Waiting for the device
Device detected :)
Mode detected: Unknown
Sorry, couldn't talk to Sahara, please reboot the device !

```
Disconnect and remove the battery to exit.

## EDL backup

Power-off the phone, boot to recovery by holding "Up" while pressing "Power",
then "Wipe cache partition", then "Wipe data/factory reset", then "power off".
Boot to edl, by holding Up + Down while pressing "Power". Execute edl commands, resetting phone manually after each, as per above.

```
$ python3.7 edl.py -loader 8110.mbn -rf backup/full_backup.img
$ python3.7 edl.py -loader 8110.mbn -printgpt | tee -a backup/printgpt.out
$ python3.7 edl.py -loader 8110.mbn -gpt backup/gpt.img
$ python3.7 edl.py -loader 8110.mbn -r recovery backup/recovery.img
$ python3.7 edl.py -loader 8110.mbn -r system backup/system.img
$ python3.7 edl.py -loader 8110.mbn -r modem backup/modem.img
...
```

## EDL restore

```
$ python3.7 edl.py -loader 8110.mbn -ws 0 backup/full_backup.img
```

## Install

Being able to install apps in KaiOS always involves using WebIDE API at lesat in the initial stages.
Classical way is using an old version of Firefox (59 or earlier) or Pale Moon  (28.6.1 or earlier),
or use the official Kaios emulator (KaiOSRT).
Alternatively you can use other command line development tools like
[XPCshell from XULRunner](https://github.com/jkelol111/make-kaios-install),
or [Gdeploy](https://gitlab.com/suborg/gdeploy), that uses NodeJS.
The easiest way for me was using [kaios-app-installer docker image](https://github.com/vkentta/kaios-app-installer):

Enable debug mode by entering ```*#*#33284#*#*```, and connect phone via usb.


```
$ git clone https://github.com/vkentta/kaios-app-installer
$ cd kaios-app-installer/
$ docker build -f Dockerfile -t vkentta/kaios-app-installer .
$ cd example_app/
$ sudo adb kill-server
$ docker run --rm -v `pwd`:/app-src --device=/dev/bus/usb:/dev/bus/usb vkentta/kaios-app-installer install_packagead

$ alias kaios-app-installer='docker run --rm -v `pwd`:/app-src --device=/dev/bus/usb:/dev/bus/usb vkentta/kaios-app-installer install_packaged'
$ kaios-app-installer

```

But then I've crafted a dirty Dockerfile for gdeploy and used it the same way:

```
$ curl https://raw.githubusercontent.com/u0d7i/TA-1071/master/gdeploy/Dockerfile | docker build --rm -t gdeploy -
$ sudo adb kill-server
$ docker run --rm --device=/dev/bus/usb:/dev/bus/usb gdeploy list
$ alias gdeploy='docker run --rm --device=/dev/bus/usb:/dev/bus/usb gdeploy'
$ gdeploy
```

## Temporarily root

Install [Wallace Toolbox](https://gitlab.com/suborg/wallace-toolbox) as per above:
```
$ git clone https://gitlab.com/suborg/wallace-toolbox
$ gdeploy install wallace-toolbox
```

![wallace-toolbox](img/wallace-toolbox.png?raw=true "wallace-toolbox")

## Recovery

```
$ sudo apt install abootimg
$ mkdir recovery
$ cd recovery/
$ cp ../backup_edl_ota_17.00.17.01/partitions/recovery.img .
$ abootimg -x recovery.img
$ abootimg-unpack-initrd
```
Mods:

```
$ curl https://gitlab.com/project-pris/recovery/-/raw/master/src/8110/root/res/keys > ramdisk/res/keys
$ curl https://gitlab.com/project-pris/recovery/-/raw/master/src/8110/root/sbin/adbd > ramdisk/sbin/adbd
$ curl https://gitlab.com/project-pris/recovery/-/raw/master/src/8110/root/sbin/busybox > ramdisk/sbin/busybox
$ chmod +x ramdisk/sbin/busybox
$ mkdir -p ramdisk/system/bin
$ for util in $(curl https://gitlab.com/project-pris/recovery/-/raw/master/bbutils.txt); do ln -sf /sbin/busybox ramdisk/system/bin/${util}; done
$ sed -i -e '/ro.debuggable=/s/=.*/=1/' ramdisk/default.prop
$ rm initrd.img
$ abootimg-pack-initrd
$ abootimg -u recovery.img -r initrd.img
```

```
$ adb reboot edl
$ python3.7 ../edl/edl.py -loader ../edl/8110.mbn -w recovery recovery.img
```

```
usb 1-8: new high-speed USB device number 56 using xhci_hcd
usb 1-8: New USB device found, idVendor=18d1, idProduct=d001, bcdDevice= 3.10
usb 1-8: New USB device strings: Mfr=1, Product=2, SerialNumber=3
usb 1-8: Product: Nokia 8110 4G
usb 1-8: Manufacturer: QUALCOMM
usb 1-8: SerialNumber: a012345b

$ adb devices
List of devices attached
a012345b        recovery

$ adb shell
/ #
```

"Mount /system"


```
/ # mount -o remount,rw /system

/ # cat /system/bin/install-recovery.sh
#!/system/bin/sh
if ! applypatch -c EMMC:/dev/block/bootdevice/by-name/recovery:15644672:c753aa63159fbd86238964e0a46c8597ad3a2d80; then
  applypatch -b /system/etc/recovery-resource.dat EMMC:/dev/block/bootdevice/by-name/boot:14774272:a4e96b2556bb82dd2c58fe71aa4c806f5129defa EMMC:/dev/block/bootdevice/by-name/recovery c753aa63159fbd86238964e0a46c8597ad3a2d80 15644672 a4e96b2556bb82dd2c58fe71aa4c806f5129defa:/system/recovery-from-boot.p && log -t recovery "Installing new recovery image: succeeded" || log -t recovery "Installing new recovery image: failed"
else
  log -t recovery "Recovery image already installed"
fi

/ # echo '#!/system/bin/sh' > /system/bin/install-recovery.sh
/ # echo 'exit 0' >> /system/bin/install-recovery.sh

/ # mount -o remount,ro /system
```

## Baseband
Have you ever wondered how and what your phone modem talks to mobile network?

[QCSuper](https://github.com/P1sec/QCSuper) is your friend. P1sec has very handy [blog post/demo](https://labs.p1sec.com/2019/07/09/presenting-qcsuper-a-tool-for-capturing-your-2g-3g-4g-air-traffic-on-qualcomm-based-phones/).

## Development
* [KaiOS dev docs](https://developer.kaiostech.com/docs/)
* [Simulator](https://developer.kaiostech.com/docs/getting-started/env-setup/simulator/)
* [@bananahackers](https://sites.google.com/view/bananahackers/development/)

## Links

* https://en.wikipedia.org/wiki/Nokia_8110_4G
* https://gerda.tech/
* https://wiki.bananahackers.net/
* https://ivan-hc.github.io/bananahackers/
* https://github.com/andybalholm/edl
* https://edl.bananahackers.net/
* https://groups.google.com/g/bananahackers - Google Groups comp.mobile.nokia.8110
* https://4pda.to/forum/index.php?showtopic=890710 (ru)
* https://4pda.to/forum/index.php?showtopic=950670 (ru)
* https://4pda.to/forum/index.php?showtopic=975097 (ru)
* https://mis.pm/banana-hack

### EDL research
* https://github.com/bkerler/edl/
* https://bkerler.github.io/2020/08/03/bring-light-to-the-darkness-p3/
* https://github.com/Zalexanninev15/emmcdl
* https://github.com/Zalexanninev15/PFT-Linux
* https://anantamaha.com/how-to-backup-firmware-from-qualcomm-android-using-qfil/
* https://wiki.bananahackers.net/development/edl
* https://github.com/andybalholm/edl
