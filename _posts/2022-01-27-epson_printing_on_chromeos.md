---
title: Epson Printing on Chrome OS
author:
  name: Aphive
  link: https://github.com/aphive
date: 2022-01-30 15:17:00
categories: [ChromeOS, Printing]
tags: [chromeos, epson, printing]
---

## My Setup

As of this writing, I am running Chrome OS 97.04692.91 and my printer is an [Epson WorkForce Pro WF-3730](https://epson.com/For-Home/Printers/Inkjet/WorkForce-Pro-WF-3730-All-in-One-Printer/p/C11CH04201). I also run [pfSense®](https://www.pfsense.org/) as my gateway but you should be able to do the same on your gateway/router.

I was trying to scan some documents as I have been working off my tablet primarily while my Laptop was down and I was waiting on some hardware to get it back up. I could find no easy way to do this and found out that Google was apparently no longer offering support for using the Epson app as they have their own built-in printer setup in the settings are. Even Epson [recommends](https://epson.com/Support/Printers/All-In-Ones/WorkForce-Series/Epson-WorkForce-Pro-WF-3730/s/SPT_C11CH04201?review-filter=Chrome+OS) going that route to setup your printer now, however, there is no integration for using the scanner in the muti-funtion/All-in-One printer world.

I forgot to book mark this during all the tabs I had open trying to figure this out but it seems that the app will not continue being supported for too much longer. I called Google support and was told there is no work around for scanning on Chrome OS other than scanning to email if your device supports it or scan to a PC then migrating the file via USB to the Chrome OS device.

## How to get it to working

### Assigning a static IP

The first thing you will want to do is assign your printer a static IP. For this you will need to get the MAC Address for the printer. To do this:

-  Connect a network cable from your gateway/router to your printer and power on the printer if you have not as yet.
-  Press the **home** button, if necessary.
-  Select **Settings**.
-  Select **General Settings**.
-  Select **Network Settings**.
-  Select **Network Status**.
-  Select **Print Status Sheet**.
-  Select **Print**.

Once you have your MAC Address, log into your router and go to the DHCP page. For me (remember I'm on pfSense), it's under **Services** → **DHCP4 Server**. Click the add button and enter the details you are asked for.

Now restart your printer and print another Network Status sheet as you did to get the MAC Address. Once you verify the printer was assigned the static IP Address, move on to the next section. If not, go back to your DHCP settings and make sure you entered everything right.

Tip:  You can also browse to IP Address in your browser so you don't have to keep going back and forth to the printer.

### Configure Chrome OS

This is the easy part.

*  Install Epson iPrint
*  Launch iPrint
*  If you did the last part correct, iPrint should automatically discover the printer. If not continue.
*  Click on the **Printer is not selected. Tap here to select a printer.** banner
*  Your printer should show up in the **Local** tab, if not ...
*  Click on the **Manual IP** tab
*  Click the **Add** button at the bottom
*  Enter the IP address you assigned the printer.
*  Click **Done**

## WF-3730 Supporting Documents

-  [WF-3730 Start Here Manual](/assets/pdf/Epson_Start_Here_Manual.pdf)
-  [WF-3730 User's Guide](/assets/pdf/Epson_User_Guide.pdf)
-  [WF-3730 Quick Guide](/assets/pdf/Epson_Quick_Guide.pdf)

## Supported Devices

Here is the list of supported Epson devices as of this writing:

### Printers and All-in-Ones for Home

-   EcoTank ET-2760 All-in-One Cartridge-Free Supertank Printer
-   EcoTank ET-3710 All-in-One Cartridge-Free Supertank Printer
-   Epson Expression Home XP-4100 Small-in-One Printer
-   Expression Home XP-4105 Small-in-One Printer
-   Expression Premium XP-6100 Small-in-One Printer
-   EcoTank ET-2720 All-in-One Supertank Printer - Black
-   EcoTank ET-2720 All-in-One Supertank Printer - White
-   WorkForce Pro WF-3733 All-in-One Printer
-   WorkForce Pro WF-3730 All-in-One Printer
-   Expression Premium XP-7100 Small-in-One Printer
-   Expression Premium XP-6000 Small-in-One Printer
-   Expression Home XP-5100 Small-in-One Printer
-   Expression ET-2750 EcoTank All-in-One Supertank Printer
-   Expression ET-3700 EcoTank All-in-One Supertank Printer
-   Expression ET-2700 EcoTank All-in-One Supertank Printer
-   Epson Expression Home XP-446 Small-in-One Printer
-   Epson Expression Home XP-340 Small-in-One All-in-One Printer
-   Epson Expression Home XP-440 Small-in-One Printer
-   Epson Expression ET-2600 EcoTank All-in-One Printer
-   Epson Expression ET-2650 EcoTank All-in-One Printer
-   Epson Expression ET-3600 EcoTank All-in-One Supertank Printer
-   Epson Expression Premium XP-640 Small-in-One All-in-One Printer
-   Epson Artisan 700 All-in-One Printer
-   Epson Artisan 725 All-in-One Printer
-   Epson Artisan 730 All-in-One Printer
-   Epson Artisan 800 All-in-One Printer
-   Epson Artisan 810 All-in-One Printer
-   Epson Artisan 835 All-in-One Printer
-   Epson Artisan 837 All-in-One Printer
-   Epson Expression Home XP-200 Small-in-One All-in-One Printer
-   Epson Expression Home XP-300 Small-in-One All-in-One Printer
-   Epson Expression Home XP-310 Small-in-One All-in-One Printer
-   Epson Expression Home XP-330 Small-in-One All-in-One Printer
-   Epson Expression Home XP-400 Small-in-One All-in-One Printer
-   Epson Expression Home XP-420 Small-in-One All-in-One Printer
-   Epson Expression Home XP-424 Small-in-One All-in-One Printer
-   Epson Expression Home XP-434 Small-in-One All-in-One Printer
-   Epson Expression Photo XP-850 Small-in-One All-in-One Printer
-   Epson Expression Photo XP-950 Small-in-One All-in-One Printer
-   Epson Expression Premium XP-520 Small-in-One All-in-One Printer
-   Epson Expression Premium XP-600 Small-in-One Printer
-   Epson Expression Premium XP-610 Small-in-One All-in-One Printer
-   Epson Expression Premium XP-620 Small-in-One All-in-One Printer
-   Epson Expression Premium XP-800 Small-in-One Printer
-   Epson Expression Premium XP-820 Small-in-One All-in-One Printer
-   Epson Expression Premium XP-830 Small-in-One All-in-One Printer
-   Epson PictureMate Charm Compact Photo Printer - PM 225
-   Epson PictureMate Dash Compact Photo Printer - PM 260
-   Epson PictureMate Deluxe Viewer Edition Compact Photo Printer
-   Epson PictureMate Flash Compact Photo Printer - PM 280
-   Epson PictureMate Pal Compact Photo Printer - PM 200
-   Epson PictureMate Snap Compact Photo Printer - PM 240
-   Epson PictureMate Zoom Compact Photo Printer - PM 290
-   Epson Stylus Photo RX580 All-in-One Printer
-   Epson Stylus Photo RX595 All-in-One Printer
-   Epson Stylus Photo RX680 All-in-One Printer

### Photo Printers for Home

-   Expression Photo XP-8600 Small-in-One Printer
-   Expression Photo XP-970 Small-in-One Printer
-   Expression Photo HD XP-15000 Wide-format Printer
-   Expression Photo XP-8500 Small-in-One All-in-One Printer
-   Epson Artisan 1430 Inkjet Printer
-   Epson Expression Photo XP-860 Small-in-One All-in-One Printer
-   Epson PictureMate PM-400 Personal Photo Lab
-   Epson PictureMate Show Digital Frame / Compact Photo Printer - PM 300
-   Epson Stylus Photo R1900 Ink Jet Printer
-   Epson Stylus Photo R260 Ink Jet Printer
-   Epson Stylus Photo R3000 Inkjet Printer
-   Epson Stylus Photo R340 Ink Jet Printer
-   Epson Stylus Photo R380 Ink Jet Printer

### Printers and All-in-Ones for Work

-   WorkForce Pro WF-7840 Wireless Wide-format All-in-One Printer
-   WorkForce Pro WF-7820 Wireless Wide-format All-in-One Printer
-   WorkForce Pro WF-4834 Wireless All-in-One Printer
-   WorkForce Pro WF-4830 Wireless All-in-One Printer
-   WorkForce Pro WF-4820 Wireless All-in-One Printer
-   WorkForce Pro WF-3820 Wireless All-in-One Printer
-   WorkForce Enterprise WF-M20590F Monochrome Multifunction Printer
-   EcoTank ET-15000 All-in-One Cartridge-Free Supertank Printer
-   WorkForce Pro WF-C878R Multifunction Color Printer
-   WorkForce Pro WF-C879R Multifunction Color Printer
-   WorkForce EC-C110 Wireless Mobile Color Printer
-   WorkForce WF-110 Wireless Mobile Printer
-   WorkForce Pro WF-C5790 Color MFP Supertank Printer
-   WorkForce Pro WF-M5799 Monochrome MFP Supertank Printer
-   WorkForce ST-M1000 Monochrome Supertank Printer
-   WorkForce ST-M3000 Monochrome MFP Supertank Printer
-   EcoTank ET-4760 All-in-One Cartridge-Free Supertank Printer - Black
-   EcoTank ET-3760 All-in-One Cartridge-Free Supertank Printer
-   EcoTank ET-4760 All-in-One Cartridge-Free Supertank Printer - White
-   Epson WorkForce WF-2830 All-in-One Printer
-   WorkForce Enterprise WF-M20590 Monochrome Multifunction Network Printer
-   WorkForce WF-2850 All-in-One Printer
-   EcoTank ET-4700 All-in-One Supertank Printer
-   EcoTank ET-M3170 Wireless Monochrome All-in-One Supertank Printer
-   EcoTank ET-M1170 Wireless Monochrome Supertank Printer
-   EcoTank ET-M2170 Wireless Monochrome All-in-One Supertank Printer
-   WorkForce ST-4000 Supertank Color MFP
-   WorkForce ST-3000 Supertank Color MFP
-   WorkForce ST-2000 Supertank Color MFP
-   WorkForce Pro EC-4040 Color Multifunction Printer
-   WorkForce Pro EC-4020 Color Multifunction Printer
-   WorkForce Pro EC-4030 Color Multifunction Printer
-   WorkForce Pro WF-C529R Workgroup Color Printer with Replaceable Ink Pack System
-   WorkForce Pro WF-C579R Workgroup Color MFP with Replaceable Ink Pack System
-   WorkForce Pro WF-M5299 Workgroup Monochrome Printer
-   WorkForce Pro WF-M5799 Workgroup Monochrome Multifunction Printer
-   WorkForce Pro WF-C8190 A3 Color Printer with PCL/PostScript
-   WorkForce Pro WF-C8690 A3 Color MFP with PCL/PostScript
-   WorkForce Pro ET-8700 EcoTank All-in-One Supertank Printer
-   WorkForce WF-2860 All-in-One Printer
-   WorkForce Pro WF-C5710 Network Multifunction Color Printer with Replaceable Ink Pack System
-   WorkForce Pro WF-C5790 Network Multifunction Color Printer with Replaceable Ink Pack System
-   WorkForce Pro WF-C5290 Network Color Printer with Replaceable Ink Pack System
-   WorkForce Pro WF-C5210 Network Color Printer with Replaceable Ink Pack
-   WorkForce WF-7210 Wide-format Printer
-   WorkForce Enterprise WF-C17590 Color Multifunction Network Printer
-   WorkForce WF-7710 Wide-format All-in-One Printer
-   WorkForce WF-7720 Wide-format All-in-One Printer
-   Expression Premium ET-7700 EcoTank All-in-One Supertank Printer
-   Expression Premium ET-7750 EcoTank Wide-format All-in-One Supertank Printer
-   WorkForce ET-3750 EcoTank All-in-One Supertank Printer
-   Epson WorkForce Pro WF-6090 Printer with PCL/PostScript
-   Epson WorkForce Pro WF-6590 Network Multifunction Color Printer
-   WorkForce Pro WF-4734 All-in-One Printer
-   WorkForce Pro WF-3720 All-in-One Printer
-   WorkForce Pro WF-4740 All-in-One Printer
-   Epson WorkForce Pro WF-4720 All-in-One Printer
-   Epson WorkForce Pro WF-4730 All-in-One Printer
-   WorkForce Pro WF-C869R Network Multifunction Color Printer
-   WorkForce Enterprise WF-C20590 A3 Color Multifunction Network Printer
-   Epson Stylus CX3800 All-in-One Printer
-   Epson Stylus CX3810 All-in-One Printer
-   Epson Stylus CX4200 All-in-One Printer
-   Epson Stylus CX4800 All-in-One Printer
-   Epson Stylus CX5000 All-in-One Printer
-   Epson Stylus CX6000 All-in-One Printer
-   Epson Stylus CX7400 All-in-One Printer
-   Epson Stylus CX7800 All-in-One Printer
-   Epson Stylus CX8400 All-in-One Printer
-   Epson Stylus CX9400Fax All-in-One Printer
-   Epson Stylus NX200 All-in-One Printer
-   Epson Stylus NX215 All-in-One Printer
-   Epson Stylus NX230 Small-in-One All-in-One Printer
-   Epson Stylus NX300 All-in-One Printer
-   Epson Stylus NX330 Small-in-One All-in-One Printer
-   Epson Stylus NX400 All-in-One Printer
-   Epson Stylus NX415 All-in-One Printer
-   Epson Stylus NX420 All-in-One Printer
-   Epson Stylus NX430 Small-in-One All-in-One Printer
-   Epson Stylus NX510 All-in-One Printer
-   Epson Stylus NX530 All-in-One Printer
-   Epson Stylus NX625 All-in-One Printer
-   Epson WorkForce 310 All-in-One Printer
-   Epson WorkForce 315 All-in-One Printer
-   Epson WorkForce 320 All-in-One Printer
-   Epson WorkForce 323 All-in-One Printer
-   Epson WorkForce 325 All-in-One Printer
-   Epson WorkForce 435 All-in-One Printer
-   Epson WorkForce 500 All-in-One Printer
-   Epson WorkForce 520 All-in-One Printer
-   Epson WorkForce 545 All-in-One Printer
-   Epson WorkForce 600 All-in-One Printer
-   Epson WorkForce 610 All-in-One Printer
-   Epson WorkForce 615 All-in-One Printer
-   Epson WorkForce 630 All-in-One Printer
-   Epson WorkForce 633 All-in-One Printer
-   Epson WorkForce 635 All-in-One Printer
-   Epson WorkForce 645 All-in-One Printer
-   Epson WorkForce 840 All-in-One Printer
-   Epson WorkForce 845 All-in-One Printer
-   Epson WorkForce ET-4500 EcoTank All-in-One Printer
-   Epson WorkForce Pro WF-4630 All-in-One Printer
-   Epson WorkForce Pro WF-8090 Network Color Printer w/ PCL/Postscript
-   Epson WorkForce Pro WF-8590 Network Multifunction Color Printer
-   Epson WorkForce Pro WF-M5194 Workgroup Monochrome Printer
-   Epson WorkForce Pro WF-R5190 Replaceable Ink Pack System
-   Epson WorkForce Pro WF-R5690 Replaceable Ink Pack System
-   Epson WorkForce Pro WF-R8590 Network Multifunction Color Printer
-   Epson WorkForce Pro WP-4010 Network Color Printer
-   Epson WorkForce Pro WP-4020 Inkjet Printer
-   Epson WorkForce Pro WP-4023 Network Wireless Color Printer
-   Epson WorkForce Pro WP-4090 Network Color Printer with PCL
-   Epson WorkForce Pro WP-4520 Network Multifunction Color Printer
-   Epson WorkForce Pro WP-4530 All-in-One Printer
-   Epson WorkForce Pro WP-4533 Network Multifunction Wireless Color Printer
-   Epson WorkForce Pro WP-4540 All-in-One Printer
-   Epson WorkForce Pro WP-4590 Network Multifunction Color Printer with PCL
-   Epson WorkForce WF-2520 All-in-One Printer
-   Epson WorkForce WF-2530 All-in-One Printer
-   Epson WorkForce WF-2540 All-in-One Printer
-   Epson WorkForce WF-2660 All-in-One Printer
-   Epson WorkForce WF-2750 All-in-One Printer
-   Epson WorkForce WF-2760 All-in-One Printer
-   Epson WorkForce WF-3540 All-in-One Printer
-   Epson WorkForce WF-3620 All-in-One Printer
-   Epson WorkForce WF-7110 Inkjet Printer
-   Epson WorkForce WF-7510 All-in-One Printer
-   Epson WorkForce WF-7520 All-in-One Printer
-   Epson WorkForce WF-7610 All-in-One Printer
-   Epson WorkForce WF-7620 All-in-One Printer

### Photo Printers for Work

-   Epson Stylus Photo R2880 Inkjet Printer

### Large Format Printers

-   Epson SureColor P400 Wide Format Inkjet Printer
-   Epson SureColor P600 Wide Format Inkjet Printer
-   Epson SureColor P800 Printer
