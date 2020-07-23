# multiboot-usb


I'm always reinstalling OS's (especially Windows) when they get bloated (I guess that's the motivation for working with containers, huh). 

With a few machines laying around and always new projects to try, I thought it'd be great to have a one-stop-stop usb to boot any and everything from.

I honestly can't believe the rabbit hole this took me down - when all I needed was grub2 and a bunch of iso's. 

The web is full of 'handy' tools to create your own multiboot flash drives but tbh, I tried a few and ... they just didn't work.

After much scraping I came across this site:

https://www.pendrivelinux.com/boot-multiple-iso-from-usb-via-grub2-using-linux/

Specifically the multiboot page (since there's yet-another-multiboot-tool there as well - but I haven't tried it (sure it's grand)) and it booted tinyOS off the bat. 

With the process sorted I collected my iso's and got to adding custom menu entries for each one.

Alas, this didn't work OOB either. There is minor debugging to complete first:

```` 
set root=$linux_boot_fs_location
````
for example:
````
grub> set root=(hd2,1)
grub> linux /boot/vmlinuz-3.13.0-29-generic root=/dev/sda1
grub> initrd /boot/initrd.img-3.13.0-29-generic
grub> boot

````

The fs couldn't be determined because hd0 was assigned to the flashdrive and the orig OS hdd had a partition on as well. Just repointed the pointer and it booted fine. No need to panic.

Will it work on a non partitioned hdd? Let's find out ... (one day)
