---
title: Rotate Linux Server Display using fbcon
author:
  name: Aphive
  link: https://github.com/aphive
date: 2022-02-11 09:17:00
categories: [Linux, Configuration]
tags: [linux, display, fbcon, servers]
---

On my wall of monitors that are hard mounted on my wall, I had one unused monitor that is in vertical (Portrait) mode that I wanted to use to plug in a server I was building out. Having to twist my head to work on the server was not going to cut it and neither was removing all the monitors around it so I can take it down or move my connections around. I had to find a way to make this work as it was without breaking my neck.

I know what you're thinking at this point, just ssh into the thing, stop making life more complicated than it needs to be.  Here's the thing, I still need to build install the OS before I can get to ssh into it and I have income generating things running on the other monitors that I need to keep up all the time so I have no other option.

Doing some research online I ran across fbcon or Framebuffer Console, from the [fbcon manpage](https://www.kernel.org/doc/Documentation/fb/fbcon.txt):

> The framebuffer console (fbcon), as its name implies, is a text console running on top of the framebuffer device. It has the functionality of any standard text console driver, such as the VGA console, with the added features that can be attributed to the graphical nature of the framebuffer.
> What are the features of fbcon? The framebuffer console supports high resolutions, varying font types, display rotation, primitive multihead, etc. Theoretically, multi-colored fonts, blending, aliasing, and any feature made available by the underlying graphics card are also possible.

Framebuffer Console allows you to control features that can be attributed to the graphical nature of the framebuffer. The framebuffer console supports high resolutions, varying font types, display rotation, primitive multihead, etc. Theoretically, multi-colored fonts, blending, aliasing, and any feature made available by the underlying graphics card are also possible.

For this purpose we’ll focus on the rotate option, `fbcon=rotate:`

This option changes the orientation angle of the console display. The value '`n`' accepts the following:

* 0 - normal orientation (0 degree)
* 1 - clockwise orientation (90 degrees)
* 2 - upside down orientation (180 degrees)
* 3 - counterclockwise orientation (270 degrees)

The angle can be changed anytime afterwards by 'echoing' the same numbers to any one of the 2 attributes found in `/sys/class/graphics/fbcon`

* `rotate` - rotate the display of the active console
* `rotate_all` - rotate the display of all consoles

Console rotation will only become available if Console Rotation Support is compiled in your kernel.

> This is purely console rotation. Any other applications that use the framebuffer will remain at their 'normal' orientation. Actually, the underlying fb driver is totally ignorant of console rotation.
{: .prompt-note }

Rotate all the frame buffers by running the following command:

> Make sure you change the rotation value to reflect the rotation of your display as noted above (options are 0 -3). Mine rotates country-clockwise so I selected clockwise (1) rotation to match. You can always try the echo command with the different options until it works if you’re not 100% sure then update GRUB to match.
{: .prompt-note }

```
echo 1 | sudo tee /sys/class/graphics/fbcon/rotate_all
```

Edit `/etc/default/grub`, find the line named `GRUB_CMDLINE_LINUX` and add `fbcon=rotate:1`, so it looks like this:

```
GRUB_CMDLINE_LINUX="fbcon=rotate:1"
```

Now run `sudo update-grub` and `sudo update-grub2` to make the change take effect.