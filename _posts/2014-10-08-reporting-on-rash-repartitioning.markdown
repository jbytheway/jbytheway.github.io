---
layout: post
title: "Reporting on rash repartitioning"
tags:
---

Recently I decided I should change the filesystem of my root partition.  This
didn't go entirely according to plan.  I tell this story as a cautionary tale
in hopes that others may be able to learn from my mistakes.

For the impatient, the most crucial lessons (in roughly decreasing order of
importance) were:

* Don't use live media which is older than your hardware.
* When making dangerous and potentially irreversible changes, be especially
  aware of [when you are
  confused](http://wiki.lesswrong.com/wiki/How_To_Actually_Change_Your_Mind#Noticing_Confusion).
* If making changes that risk making your computer unbootable, make sure you
  have another computer on hand to help fix it.
* If you have difficulty booting from live media, think very carefully before
  taking any action which might prevent normal booting also.
* There is [more than one way to make a partition
  table](http://www.funtoo.org/GUID_Booting_Guide).
* There is [more than way to boot](http://www.funtoo.org/UEFI_Install_Guide).
* Booting a live CD in rescue mode can actually be useful.
* When in doubt, Debian is a reliable and convenient basis from which to
  operate.
* [`apt-file`](http://en.wikipedia.org/wiki/Apt-file) is still awesome.

This all started with some mysterious file corruption in my root partition.  I
am still not sure what might have caused it, but the two most obvious
candidates were the filesystem and the hardware.  I figured that changing the
filesystem was relatively easy, and I should try that first.

This ought to be easy.  I've messed around with partitions before.  Although I
know resizing of partitions is always flagged as dangerous, I've never had any
trouble before, so the next time I was rebooting my computer, I decided to do
it.

I had prepared a [live USB
stick](http://www.sysresccd.org/Sysresccd-manual-en_How_to_install_SystemRescueCd_on_an_USB-stick)
of [SystemRescueCd](http://www.sysresccd.org/).  But when I tried to use it, I
had no luck.  At the time I assumed I'd just made the USB stick incorrectly.  I
later learnt that this was because my BIOS was attempting to use
[UEFI](http://en.wikipedia.org/wiki/Unified_Extensible_Firmware_Interface) to
boot from the thing, which is supposed to work, but didn't.

In any case, unknowing, I decided to simply use an older SystemRescueCd live CD
I burnt years ago.  This was my **biggest mistake**.

I resized the partition with gparted to make space for another.  I didn't try
to make another partition yet, or copy any data.  I wanted to do as much as
possible inside my normal environment.  I ignored the fact that my disk
contained a mysterious extra partition whose purpose was unclear.  My confusion
here was a clue, and ignoring it was another serious mistake.

Everything looked fine, and I rebooted.

Nothing.

After the BIOS detected the disks, I was dumped to an empty screen.  No GRUB.

I figured I needed to reinstall GRUB.  I booted back into the live CD, but I
was unable to chroot into my regular environment.  The `chroot` binary was 32
bit, and my system was 64 bit.  Whoops.

I tried another live CD, this one a Gentoo installation image which was
certainly 64 bit throughout.  This time `chroot` failed with `Illegal
instruction`.  I still have no real idea what was going on here, but my best
guess is that it is a consequence of all my executables being compiled from
source specifically for my CPU, and that CPU instruction set being newer than
this live CD.  Or it may have been because I wasn't mounting `/proc`, `/sys`,
and `/dev` properly before chrooting.

Worse yet, both live CDs lacked support for my network card, so my Internet access was reduced to just my phone, and I could not acquire a newer image.

At this point it was clear I was in serious trouble.  It was also quite late,
and from previous similar experience I have a personal rule never to attempt to
fix a computer that won't boot after midnight.  It causes gremlins.

The next day I gained access to another computer, and made a new live USB
stick.  This time I used a [live Debian image](http://live.debian.net/) and was
able to confirm that it was bootable.

But it still didn't work on my desktop.  Now I knew it wasn't a problem with
the USB stick, and I explored the BIOS more carefully.  When I scrolled all the
way to the bottom of the (surprisingly long) list of boot options I
discovered the non-UEFI version of the USB stick, and, Hey Presto!, it worked.

Sort of.

At least I got through GRUB, but the boot process crawled to a halt and was
riddled with error messages.  My heart sank.

Booting in rescue mode worked a little better, and made it clear (from the
kernel errors that kept popping up) that the problem was in the USB system
somewhere.  Some experimental unplugging of my various bits and bobs fixed it,
and finally I was booted into a modern, useful Linux system!

(I'm not sure what this problem was either; my best guess is that the live
Debian was loading the wrong driver for something.)

When I consulted the [Funtoo installation
guide](http://www.funtoo.org/Funtoo_Linux_Installation) for reminders on how to
reinstall GRUB, I discovered the source of my original problem.  When I set up
this machine I had used a [GPT partitioning
scheme](http://en.wikipedia.org/wiki/GUID_Partition_Table).  I had quite
forgotten such things existed, and the version of parted which had messed with
the partition table for me didn't know about them either.  It was too old.  I
should have had a 'protective MBR' which might perhaps have prevented this, but
I am not surprised that this didn't work.  The extra little partition I had
noticed earlier is used by GRUB in this configuration to store some of itself.

Armed with a fully-featured Debian, it took only a few checks with
[`apt-file`](http://en.wikipedia.org/wiki/Apt-file) to get me the tools I
needed to create my new partition, fix the partition table, reinstall GRUB,
chroot into my Funtoo installation, recompile my kernel (because it now needed
support for my new root filesystem), and reboot.  Everything went smoothly.

However, at some point during this whole process I accumulated some more
filesystem corruption.  Of course, I can still blame the old filesystem for
now.  But if it happens again, I may have to buy a new disk and go through
this whole process again.
