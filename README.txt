A script to make my life easier when dealing with my windows partition.

I want to use the same foobar2000 configuration from Ubuntu and Windows,
which means installing it on the Windows side and running it under Wine from
the Windows partition in Ubuntu.  Of course, this means the Windows
partition has to be mounted first, but I didn't want to just automount it at
startup by changing the fstab file.  I want to integrate foobar into the
launcher, so I didn't want to have to sudo every time I start the thing.

mount/umount couldn't be used since they require root privileges (unless I
indicate otherwise in fstab, but then the ntfs driver gets mad at me.  I
could allow myself to mount anything at any time through the sudoers file,
but I don't like that either). Luckily, udisks allows me to mount/unmount 
without root.  However, you can't specify a custom mount point, and the
default one is gross and based on the UUID.

So, I made this script that will mount my windows partition before running a
given command, and then unmount it afterwards (assuming it wasn't already
being used before the script ran, and nobody else started using it while the
command was running).  It will make a symlink at /mnt/windows pointing to
the yucky default mount point, so I have a friendlier way to get to it.

