+++
date = "2017-05-17T13:24:11+03:00"
draft = false
title = "How to safely retrieve files from failing HDD, SSD or SD card using free tools"
tags = ["data", "recovery", "reliable", "free", "photography"]
+++

All the drives we are using to store our precious photos and videos are not 100% reliable. Everybody should know that and
back everything up but even if you are doing it properly, there are cases when drive fails
and you have nowhere to get its contents except from the drive itself.

It happened to me recently. 23 GB SD card from a trip almost full of precious shots was corrupted when inserted
into a cheap PC card reader.

As a result, both Windows PC and Mac were unable to read anything from the card and were prompting to format it instead.
After trying lots of commercial software designed specifically for recovering photos and files from SD cards I was lost.
None worked well. One of the tools was able to recover some photos. About 2% of what was there initially.

![A fox in the wild. Bygdøy, Oslo](/img/posts/photo_fox.jpg)

I did not give up and finally found out how to do it properly and, surprisingly, for free.

First, drive may degrade so it is a bad idea to try reading from it repeatedly. It may fail and die
entirely. We need a tool to copy entire drive to an image file on a local disk byte by byte reading as much as we can.
Such a tool exists and is called [GNU Ddrescue](https://www.gnu.org/software/ddrescue/). The only con of it is that it
requires MacOS or Linux to run but it is not a problem since there are live CDs available. In particular, there is
[Knoppix](http://www.knopper.net/knoppix/index-en.html) which has all the tools bundled.

So we are opening console and trying to find out which drives we have. In order to do it use
`fdisk -l` on Linux and `diskutil list` on MacOS. On MacOS prefer disk names which start with
`/dev/r` which are raw disks with buffer-less communication.

Now, as you know drive names:

```
# get most of the error-free data quickly
./ddrescue -n /dev/old_disk /mnt/sdb1/bad_drive.img rescued.log
# then attempt to get data which is in bad areas
./ddrescue -r 1 /dev/old_disk /mnt/sdb1/bad_drive.img rescued.log
```

`/mnt/sdb1/bad_drive.img` is a path to image file to create. Obviously, it should be on another disk and you should
have at least the same amount of space available as the side of original disk you are restoring.

As it is done, we need to actually get our data from the disk image we have. There is another tool for that called
[PhotoRec](http://www.cgsecurity.org/wiki/PhotoRec). Again, it is a console tool.

Launch it as `./photorec /mnt/sdb1/bad_drive.img` then
[follow instructions](http://www.cgsecurity.org/wiki/PhotoRec_Step_By_Step). At this point you can try various options
as many times as you want since image file is not affected and is on a well working drive so there is little chance to
lose data because of messing with original drive.

That is it. Using these two tools I was able to recover all the precious photos from corrupted SD card.

![Someone parked right at the pier. Aker Brygge, Oslo](/img/posts/photo_mustang.jpg)

- Article was [reposted at PetaPixel](https://petapixel.com/2017/05/18/safely-retrieve-files-off-failing-hdd-ssd-sd-cards-using-free-tools/).