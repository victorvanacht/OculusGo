# OculusGo
Meta Oculus Go related

## Unlocking Oculus Go ("Rooting")

Before obsoleting the Oculus Go, Meta release one **final** firmware version for the device, that 'unlocks' it (allows root access).
This firmware has exactly the same functionality as previous verions, except for 2 very import points:

* It allows access from a PC via USB for tools such as ADB, without having a special *developer account* from Meta.
* It allows root access to the device

You can download this firmware here: [https://developers.meta.com/horizon/blog/unlocking-oculus-go/](https://developers.meta.com/horizon/blog/unlocking-oculus-go/)
But for your convenience (and when Meta decides to remove this webpage again, you can also find it in this repository) in the folder ``UnlockedFirmware``.

There is absolutely no risk in installing the unlocked firmware on your Oculus Go. Because this unlocked firmware is (still) digitally encrypted and signed by Meta (otherwise it could not be installed on a 'locked' Oculus Go.)

It is only *after* the [actual unlocking](#the-actual-unlocking-of-the-oculus-go) that there is a theoretical risk that the Oculus Go is vulnerable for hackers. Because *after* unlocking it, it is (theoretically) possible to install rogue apps.

### Instructions

#### Prerequisites
1. Make sure to have [git](https://git-scm.com/install/) installed on your computer.
2. Make sure to have [git lfs](https://git-lfs.com/) installed on your computer. Git lfs (Large File System) is required because this Github repository contains some very large files (such as firmware images) that the standard git does not support. You can install git lfs simply by opening a command prompt and type
```
git lfs install
```

3. Clone this github repository from github to a local folder on your computer. Cloning may take a while, because of some of the large files (> 800MByte). In the previous command shell you can type:
```
c:
cd \
git clone https://github.com/victorvanacht/OculusGo.git
```
4. You can go into the cloned repository folder by typing:
```
cd OculusGo
```
5. Also make sure you have Google's Android USB drivers installed. You can download them from here: 
[https://developer.android.com/studio/run/win-usb](https://developer.android.com/studio/run/win-usb).
But you can also find them in the ```usb_driver``` folder of this repository. 
Install the driver by opening a Windows Explorer, browsing to the folder where you just cloned the repositoy (```C:\OculusGo``` in this example). Then browse into the folder ```usb_driver``` and right-click with your mouse on the file ```android_winusb.inf```.
And select ```install``` from the contect menu.
When you have a USB cable connected and are in the bootloader menu (see the section [below](#downloading-the-unlocked-firmware-on-the-oculus-go)), you may want to check the Windows Device Manager for any exclamation marks for unknown USB-devices. If so, right-click on the device, select ```Update driver```. Then select ```Browse my computer for drivers```. Then select ```Let me pick from a list```. And then scroll to ```Google Android``` (or something similar). You may get a warning that these are not the right drivers for your device (Oculus Go) because they are from Google for generic Android edvices, but continue anyway.



#### Downloading the unlocked firmware on the Oculus Go


Make sure the battery of the Oculus Go is fully charged, so the update does not fail half-way because of a depleted battery.

1. Make sure the Oculus Go is completely switched off. By holding down the power button for some time and selecting ```Power off```.
2. Next, start the Oculus Go in bootloader-mode. Do this by first pressing AND HOLDING the volume-**down** button on the headset and the press AND HOLD the power button, until the boot menu appears. When the boot menu appears you can release both buttons.
3. Connect the Oculus Go headset to your PC with a USB cable.
4. You can navigate through the options of the boot menu using the volume-down and volume-up bottons. You can select an option by pressing the power button. The options are:
    * Exit and boot the device
    * Factory reset
    * Enable sideloading update
    * Power off
5. Navigate to the option ```Enable sideloading update``` by using the volume-up and volume-down buttons and select it by pressing the power button. The screen of the Oculus Go now turns dark, and it is ready to receive new firmware.
6. If you still have the command shell open from the previous section, you can skip this step. Otherwise open a new command window on your PC and type:
```
c:
cd \OculusGo
```
7. Next, type in the command window on your PC:
```
.\AndroidPlatformTools\platform-tools-windows\adb sideload .\UnlockedFirmware\Oculus_Go_SW_Unlock_v1\unlocked_build.zip
```
Maybe you have to give ADB acces on your computer to networks. Please do so.
On the Oculus Go headset you will see: ```Installing system update```
and a progress bar that slowly runs from 0% to 100%.

On the PC you will see somthing like this: 
```
daemon not running; starting now at tcp:5037
daemon started successfully
serving: '.\UnlockedFirmware\Oculus_Go_SW_Unlock_v1\unlocked_build.zip'  (~0%)
```
where the progress is also slowly counting from 0% to 100%.

After uploading has finished, the Oculus Go will reboot. You will not see any difference with any previous firmware version.

#### The actual unlocking of the Oculus Go

1. Enter the Oculus Go in bootloader-mode again, by repeating steps 1 and 2 from the [previous section](#downloading-the-unlocked-firmware-on-the-oculus-go).

2. In the bootloader menu, do not select any option. Just keep the boot menu open.

3. If you still have the command shell open from the previous section, you can skip this step. Otherwise open a new command window on your PC and type:
```
c:
cd \OculusGo
```
4. Next, perform the actual unlocking of the Ocuslus Go. 
**This step will factory reset your device!!!**. 
Type in the command window on your PC:
```
.\AndroidPlatformTools\platform-tools-windows\fastboot oem unlock
```
When on your PC you get message like ```<waiting for device>```, there might be something wrong with the Android USB drivers.
Please recheck step 5 of the [Prerequisites](#prerequisites) 

5. After successful completion of this command, the Oculus Go will restart.

6. You can see that unlocking of the Oculus Go was succesful when after every power-on an additional warning screen with ugly orange letters appears just before booting the device. This warning screen will disappear after 5 seconds, and the Oculus Go will continue to boot.

7. In case you ever want to lock your Oculus Go again, you can repeat steps 1-3 and then in the command window type:
```
.\AndroidPlatformTools\platform-tools-windows\fastboot oem lock
```
