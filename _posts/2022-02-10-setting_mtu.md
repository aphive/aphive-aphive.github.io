---
title: Configuring MTU
author:
  name: Aphive
  link: https://github.com/aphive
date: 2022-02-10 15:17:00
categories: [Networking, MTU]
tags: [networking, configuration, mtu]
---

I recently had some issues with networking on a computer and one advice I got was to check the MTU setting. This isn't something that one would normally need to mess with but it does apparently come up every now and again and there isn't much information on how to do this unless you are a network engineer.  Looking online I came across this old tutorial that is no longer available and thought I'd resrrect it for my reference and for others that may encounter the need to adjust their MTU settings.

> This is copied verbatim from the original poster with a few formatting changes only
{: .prompt-note }

## How to determine the Max MTU size for an optimal internet connection

Information on the Internet is transferred in packets. The MTU setting controls the maximum Ethernet packet size your PC or Router will send.
Although larger packets can be constructed and sent, your ISP and Internet backbone routers and equipment will chop up (fragment) any packets larger than their limit. These parts are then reassembled by the target equipment before reading. This fragmentation and reassembly is not optimal.

### MTU and Windows and Defaults

Windows default MTU is 1500, or 576 for external networks. 1500 is OK unless you are running PPPoE, want to use IPSec (Secure VPN's) or both, then it's too big. 576 is too small, and inefficient for broadband Internet!

### Procedure to find optimal MTU

If your MTU is currently set too low, for example 576, the following procedure will not be able to detect whether you have discovered the "Optimal MTU size". First reset the MTU setting of your equipment to 1500, the maximum size it could possibly be. For PPPoE, your Max MTU should be no more than 1492 to allow space for the 8 byte PPPoE "wrapper”. 1492 + 8 = 1500. From there it is possible to experiment and find the optimal MTU value. For PPPoE, the stakes are high: if you get your MTU wrong, you may not just be sub-optimal, things like uploading files, or the loading of web pages may stall, or not work at all! The ping test we will be doing does not include the IP/ICMP header of 28 bytes. 1500 – 28 = 1472. Include the 8 byte PPPoE wrapper if your ISP uses PPPoE and you get 1500 – 28 – 8 = 1464. The reason for these numbers will be apparent very soon.

To find out if your packets are getting fragmented, we use a Ping command from the command prompt.

The best value for MTU is that value just before your packets get fragmented. Add 28 to the largest packet size that does not result in fragmenting the packets (since the ping command specifies the ping packet size, not including the IP/ICMP header of 28 bytes), and this is your Max MTU setting.

### Windows

Go to Start → Programs → Accessories → Command Prompt and type (or Copy and Paste) the following:

* If you connect to your ISP using PPPoE:
```
ping -f -l 1464 www.dslreports.com
```
* If you are not connecting to your ISP through PPPoE:
```
ping -f -l 1472 www.dslreports.com
```

> That is a dash lower case "L," not a dash "1." Also note the spaces in between the sections.
{: .prompt-note }

### Linux

Open your Terminal and use the following options:

* If you connect to your ISP using PPPoE:
```
ping -s 1464 www.dslreports.com
```
* If you are not connecting to your ISP through PPPoE:
```
ping -s 1472 www.dslreports.com
```

### macOS

Open your Terminal and use the following options:

* If you connect to your ISP using PPPoE:
```
ping -D -s 1464 www.dslreports.com
```
* If you are not connecting to your ISP through PPPoE:
```
ping -D -s 1472 www.dslreports.com
```

> Linux and OS X commands ARE case sensitive.
{: .prompt-warning }

### Next

Press <kbd>Enter</kbd>

* If you get the `packet needs to be fragmented` error message, then reduce the initial 1464 / 1472 by 10 until you no longer get the error message. Then increase the setting by 1 until you are 1 away from (less than) getting the packet needs to be fragmented error message again.
* If you can ping through with the number at 1464 (for PPPoE) / 1472 (for non-PPPoE), with no error message, you are done! Stop.
* Add 28 to the highest number pinged with no error (for both PPPoE and non-PPPoE), and that sum is your Max MTU setting. Use that (calculated sum) Max MTU setting in your router, or on your PC if your PC connects directly to your modem.

## Reference
The original site is no longer up and this was only located on the WayBack Machine [here](https://web.archive.org/web/20180627061040/http://www.bestyoucanget.com/optimizemtu.htm).