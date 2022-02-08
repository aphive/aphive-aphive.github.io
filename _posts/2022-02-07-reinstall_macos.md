---
title: Reinstalling macOS
author:
  name: Aphive
  link: https://github.com/aphive
date: 2022-02-07 15:17:00
categories: [Apple, macOS]
tags: [apple, macos, install]
---

We've all gotten to the point where our computer needs a refresh, happens with Windows, it happens with Linux and it sure as heck happens with macOS as well. Either you mess something up, it's starting to show its age or you are planning on selling it or giving it away.

This article will cover how to create an install media as well as wipe and reinstall macOS, it will not go over backing up your data, you should know how to do that or should know how to search online for instructions.

## Creating a bootable installer

* A USB flash drive or other secondary volume formatted as Mac OS Extended, with at least 14GB of available storage
* A downloaded installer for macOS Monterey, Big Sur, Catalina, Mojave, High Sierra, or El Capitan

### Download macOS

* Download: [macOS Monterey](https://apps.apple.com/us/app/macos-monterey/id1576738294?mt=12), [macOS Big Sur](https://apps.apple.com/us/app/macos-big-sur/id1526878132?mt=12), [macOS Catalina](https://apps.apple.com/us/app/macos-catalina/id1466841314?mt=12), [macOS Mojave](https://apps.apple.com/us/app/macos-mojave/id1398502828?mt=12), or [macOS High Sierra](https://apps.apple.com/us/app/macos-high-sierra/id1246284741?mt=12)
    * These download to your Applications folder as an app named Install macOS version_name. If the installer opens after downloading, quit it without continuing installation. To get the correct installer, download from a Mac that is using macOS Sierra 10.12.5 or later, or El Capitan 10.11.6. Enterprise administrators, please download from Apple, not a locally hosted software-update server.
* Download: [OS X El Capitan](http://updates-http.cdn-apple.com/2019/cert/061-41424-20191024-218af9ec-cf50-4516-9011-228c78eda3d2/InstallMacOSX.dmg)
    * This downloads as a disk image named InstallMacOSX.dmg. On a Mac that is compatible with El Capitan, open the disk image and run the installer within, named InstallMacOSX.pkg. It installs an app named Install OS X El Capitan into your Applications folder. You will create the bootable installer from this app, not from the disk image or .pkg installer.

### Use the 'createinstallmedia' command in Terminal

* Connect the USB flash drive or other volume that you're using for the bootable installer.
* Open **Terminal**, which is in the **Utilities** folder of your **Applications** folder.
* Type or paste one of the following commands in Terminal. These assume that the installer is in your Applications folder, and MyVolume is the name of the USB flash drive or other volume you're using. If it has a different name, replace MyVolume in these commands with the name of your volume.

#### Monterey:*

```
sudo /Applications/Install\ macOS\ Monterey.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume
```

#### Big Sur:*

```
sudo /Applications/Install\ macOS\ Big\ Sur.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume
```

#### Catalina:*

```
sudo /Applications/Install\ macOS\ Catalina.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume
```

#### Mojave:*

```
sudo /Applications/Install\ macOS\ Mojave.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume
```

#### High Sierra:*

```
sudo /Applications/Install\ macOS\ High\ Sierra.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume
```

#### El Capitan:

```
sudo /Applications/Install\ OS\ X\ El\ Capitan.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolume --applicationpath /Applications/Install\ OS\ X\ El\ Capitan.app
```

* If your Mac is using macOS Sierra or earlier, include the `--applicationpath` argument and installer path, similar to the way this is done in the command for El Capitan.


After typing the command:

* Press <kbd>Return</kbd> to enter the command.
* When prompted, type your administrator password and press <kbd>Return</kbd> again. Terminal doesn't show any characters as you type your password.
* When prompted, type <kbd>Y</kbd> to confirm that you want to erase the volume, then press <kbd>Return</kbd>. 
    * Terminal shows the progress as the volume is erased.
* After the volume is erased, you may see an alert that Terminal would like to access files on a removable volume.
* Click OK to allow the copy to proceed.
* When done, the volume will have the same name as the installer, such as **Install macOS Monterey**.
    * You can now quit Terminal and eject the volume.

## Using the bootable installer

Determine whether you're using a Mac with Apple silicon _(see **Mac computers with Apple silicon** below)_, then follow the appropriate steps:

### Apple silicon

* Plug the bootable installer into a Mac that is connected to the internet and compatible with the version of macOS you're installing.
* Turn on your Mac and continue to hold the power button until you see the startup options window, which shows your bootable volumes.
* Select the volume containing the bootable installer, then click Continue.
* When the macOS installer opens, follow the onscreen instructions.

### Intel processor

* Plug the bootable installer into a Mac that is connected to the internet and compatible with the version of macOS you're installing.
* Press and hold the <kbd>alt ⌥</kbd> key immediately after turning on or restarting your Mac.
* Release the Option key when you see a dark screen showing your bootable volumes.
* Select the volume containing the bootable installer. Then click the up arrow or press Return.
* If you can't start up from the bootable installer, make sure that the External Boot setting in Startup Security Utility _(see **Startup Security Utility** below)_ is set to allow booting from external media.
* Choose your language, if prompted.
* Select Install macOS (or Install OS X) from the Utilities window, then click Continue and follow the onscreen instructions.

## Extra Information

### Mac computers with Apple silicon

* MacBook Pro (14-inch, 2021)
* MacBook Pro (16-inch, 2021)
* iMac (24-inch, M1, 2021)
* Mac mini (M1, 2020)
* MacBook Air (M1, 2020)
* MacBook Pro (13-inch, M1, 2020)

### Startup Security Utility

If you're using a Mac with the Apple T2 Security Chip, Startup Security Utility offers three features to help secure your Mac against unauthorized access: Firmware password protection, Secure Boot, and the ability to set allowed boot media.

#### Open Startup Security Utility

* Turn on your Mac, then press and hold <kbd>Command ⌘</kbd>+<kbd>R</kbd> immediately after you see the Apple logo. Your Mac starts up from macOS Recovery.
* When you're asked to select a user you know the password for, select the user, click Next, then enter their administrator password.
* When you see the macOS utilities window, choose Utilities > Startup Security Utility from the menu bar.
* When you're asked to authenticate, click Enter macOS Password, then choose an administrator account and enter its password.

#### Set a firmware password

You can use a firmware password to prevent anyone who doesn't have the password from starting up from a disk other than your designated startup disk. To set a firmware password in Startup Security Utility, click Turn On Firmware Password, then follow the onscreen instructions. Learn more about firmware passwords.

You can also disallow booting from external or removable media to prevent even those who know the firmware password from starting up from such media.


#### Change Secure Boot settings

Use these settings to make sure that your Mac always starts up from a legitimate, trusted operating system.

**Full Security**

Full Security is the default setting, offering the highest level of security.

During startup, your Mac verifies the integrity of the operating system (OS) on your startup disk to make sure that it's legitimate. If the OS is unknown or can't be verified as legitimate, your Mac connects to Apple to download the updated integrity information it needs to verify the OS. This information is unique to your Mac, and it ensures that your Mac starts up from an OS that is trusted by Apple.

If FileVault is enabled while your Mac is attempting to download updated integrity information, you're asked to enter a password to unlock the disk. Enter your administrator password, then click Unlock to complete the download.

* If the OS doesn't pass verification:
    * macOS: An alert informs you that a software update is required to use this startup disk. Click Update to open the macOS installer, which you can use to reinstall macOS on the startup disk. Or click Startup Disk and choose a different startup disk, which your Mac will also attempt to verify.
    * Windows: An alert informs you that you need to install Windows with Boot Camp Assistant.
* If your Mac can't connect to the internet, it displays an alert that an internet connection is required.
    * Check your internet connection, such as by choosing an active network from Wi-Fi status menu  in the menu bar. Then click Try Again.
    * Or click Startup Disk and choose a different startup disk.
    * Or use Startup Security Utility to lower the security level

**Medium Security**

During startup when Medium Security is turned on, your Mac verifies the OS on your startup disk only by making sure that it has been properly signed by Apple (macOS) or Microsoft (Windows). This doesn't require an internet connection or updated integrity information from Apple, so it doesn't prevent your Mac from using an OS that is no longer trusted by Apple.

* If the OS doesn't pass verification:
    * macOS: An alert informs you that a software update is required to use this startup disk. Click Update to open the macOS installer, which you can use to reinstall macOS on the startup disk. This requires an internet connection. Or click Startup Disk and choose a different startup disk, which your Mac will also attempt to verify.
    * Windows: An alert informs you that you need to install windows with Boot Camp Assistant.

**No Security**

No Security doesn't enforce any of the above security requirements for your startup disk.

### Set allowed boot media

Use this feature to control whether your Mac can start up from external or removable media. The default, most secure setting is to disallow it. If you attempt to boot from such media and you get a warning that your security settings do not allow it, you can change the setting in Startup Security Utility.

Your Mac doesn't support booting from network volumes, whether or not you allow booting from external or removable media.
