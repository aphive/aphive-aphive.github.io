---
title: Gaming with pfSense
author:
  name: Aphive
  link: https://github.com/aphive
date: 2022-02-01 15:17:00
categories: [Gaming, pfSense]
tags: [gaming, xbox, pc, pfsense]
---

I'm an avid Xbox gamer, started back in the early days with Halo and the OG Xbox. Today I own two consoles that me and my son play on and he owns a PS4 Pro and a PC to game on with his buds.

As you know from my previous post, I run pfSense as my gateway so I needed to do some tweaking to get things working properly.

## Getting Started

First thing you need to do is gather your MAC Addresses for each device.

### Xbox

* Navigate to the **Settings** page
* Select **Network**
* Select **Advanced Settings**
* Select which MAC you want to use, I suggest going Wired to reduce latency but it's up to you.

### Playstation

* Locate the **Settings** icon on your Dashboard toolbar
* Select the **System** icon from the list
* Choose **System Information** from the toolbar
* You should see your console's wireless MAC address

### PC

* Right-click on the **Start button** and select **Command Prompt** from the menu
* Type in `ipconfig /all` and press Enter. Your network configurations will display
* Scroll down to your network adapter and look for the values next to **Physical Address**

### Nintendo Switch

* Select **System Settings** from the HOME Menu.
* Scroll down through the menu and select **Internet**.
* The Nintendo Switch console's MAC address will be listed under **System MAC Address**.

## Configure pfSense

### Enable Static DHCP

* Click **Services** → **DNS Resolver**
* Enable  **DHCP Registration**
* Enable  **Static DHCP**

### Setting Static IPs

* Log into pfSense
* Click **Services** → **DHCP Server**
* Scroll to the bottom of the page
* Click **Add**
* Fill in the following:
    * MAC Address
    * IP Address
    * Hostname
    * Enable ARP Table Static Entry
    * Click **Save**

### Setting up Firewall Rules

* Click **Firewall** → **Aliases**
* Fill in in the fields:
    * Name: `Gaming`
    * Type: `Hosts`
    * Host(s): add as many hosts as you have using the IP addresses you assigned and add a description for each.
        * Click **Add Host** to add more hosts
* Click **Save**

* While still logged into pfSense
* Click **Firewall** → **NAT** → **Outbound**
* Change **Outbound NAT Mode** to `Hybrid Outbound NAT rule generation. (Automatic Outbound NAT + rules below)`
* Click **Save**
* Under **Mappings**, click **Add**
* Set the Following:
    * Interface: `WAN`
    * Address Family: `IPV4` _I don't use IPV6_
    * Protocol: `any`
    * Source: Set Type to `Network`, set Source to your alias `Gaming / 32`
    * Destination: `Any`
    * Address: `Interface Address`
    * Port or Range : Enable `Static Port`
    * Description: Give the rule a description, ex: `Gaming NAT`
* Click **Save**

###  UPnP / NAT-PMP

Many have concerns about this protocol, and they are well warranted, but it has become a staple in networking.

UPnP (Universal Plug and Play) is a service that allows devices on the same local network to discover each other and automatically connect through standard networking protocols (such as TCP/IP HTTP, and DHCP). Some examples of UPnP devices are printers, gaming consoles, WiFi devices, IP cameras, routers, mobile devices, and Smart TVs. Many games today require this to properly connect. With enabled UPnP, devices directly forward a port on your router and save you from manually forwarding ports.

**By default, most new routers come with UPnP enabled and many users are unaware that they're at risk of a malware infection or a data breach.**

UPnP can also modify router settings to open ports into a firewall to facilitate the connection of devices outside of a network.

* While still logged into pfSense
* Click **System** → **UPnP & NAT-PMP**
* Click the following check boxes:
    * Enable
    * UPnP Port Mapping
    * NAT-PMP Port Mapping
* In  ACL Entries, add `allow 53-65535 192.168.1.12/32 53-65535`
    * Click **Add** to add each device
* Click **Save**



* Click **System** → **Advanced** → **Firewall & NAT**
* Look for and set NAT Reflection mode for port forwards to `Pure NAT`
* Look for and enable Enable automatic outbound NAT for Reflection
* Click **Save**

## UPnP Concerns

The UPnP service becomes dangerous if it establishes connections with devices that are infected with malware. Such connections make DDoS attacks possible.

The U.S Department of Homeland Security urged all businesses to disable their UPnP following a [cyberattack](https://www.zdnet.com/article/millions-of-pcs-exposed-through-network-bugs-security-researchers-find/) in 2013 impacting tens of millions of devices. The National Institute of Standards and Technology (NIST) hosts a continuously updated list of Common Vulnerability Exposures (CVEs) for popular devices and software solutions that can be accessed [here](https://nvd.nist.gov/vuln/full-listing).

More details about UPnP-specific vulnerabilities can be found on the [Carnegie Mellon University website](https://www.kb.cert.org/vuls/id/339275).


## Required Ports

This is why things get complicated without UPnP. This is not an exhaustive list of all the required ports for each gaming platform or game, it's just an example of why UPnP is needed and the complexity you would need to go through to setup manual port forwarding if you're a gamer.


### Destiny 2

* Playstation 4
    * TCP: 1935, 3478-3480
    * UDP: 3074, 3478-3479
*  Xbox One
    * TCP: 3074
    * UDP: 88, 500, 1200, 3074, 3544, 4500
* PC
    * TCP:
    * UDP: 3074, 3097
* Steam
    * TCP: 27015-27030, 27036-27037
    * UDP: 3074, 3097, 4380, 27000-27031, 27036
* Xbox Series X
    * TCP: 3074
    * UDP: 88, 500, 1200, 3074, 3544, 4500
* Playstation 5
    * TCP: 1935, 3478-3480
    * UDP: 3074, 3478-3479

### Call of Duty

* PC
    * TCP: 3074, 27014-27050
    * UDP: 3074, 3478, 4379-4380, 27000-27031, 27036
* Playstation 4
    * TCP: 1935, 3478-3480
    * UDP: 3074, 3478-3479
* Xbox One
    * TCP: 3074
    * UDP: 88, 500, 3074-3075, 3544, 4500

### Xbox Live

* Xbox One
    * TCP: 53, 80, 3074
    * UDP: 53, 88, 500, 3074, 3544, 4500
* PC
    * TCP: 53, 80, 3074
    * UDP: 53, 88, 500, 3074, 3544, 4500
* Xbox Series X
    * TCP: 53, 80, 3074
    * UDP: 53, 88, 500, 3074, 3544, 4500
* Xbox 360
    * TCP: 53, 80, 1863, 3074
    * UDP: 53, 88, 1863, 3074

### PlayStation Network - Default

* General
    * TCP: 3478-3480
    * UDP: 3478-3479
* Playstation 5
    * TCP: 1935, 3478-3480
    * UDP: 3074, 3478-3479

### Halo Infinite

* PC
    * TCP: 3074
    * UDP: 88, 500, 3074-3075, 3544, 4500
* Xbox One
    * TCP: 3074
    * UDP: 88, 500, 3074-3075, 3544, 4500
* Steam
    * TCP: 3074, 27015, 27036
    * UDP: 88, 500, 3074-3075, 3544, 4500, 27015, 27031-27036
* Xbox Series X
    * TCP: 3074
    * UDP: 88, 500, 3074-3075, 3544, 4500

### Halo: The Master Chief Collection

* Xbox One
    * TCP: 3074
    * UDP: 88, 500, 3074, 3544, 4500
* PC
    * TCP: 3074
    * UDP: 88, 500, 3074, 3544, 4500
* Steam
    * TCP: 3074, 27015, 27036
    * UDP: 88, 500, 3074, 3544, 4500, 27015, 27031-27036
* Xbox Series X
    * TCP: 3074
    * UDP: 88, 500, 3074, 3544, 4500


Just to play with the above in consideration you would need to port forward 69 ports individually. You see how that can become a chore, considering many homes have more than one gaming devices.
