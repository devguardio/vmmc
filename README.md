# vmmc
virtual sd card actually backed by ceph block storage

booting arm boards in starfeld is currently done from local emmc. We do not have backups of the emmc as user data is on ceph anyway.
But customers doing custom kernels HAVE to flash it on emmc, because some bootloaders only support sdcard boot.

So we'll bring the emmc to ceph as well.

### FGPA

an fgpa receives sd commands and translates it into usb commands.
since sd is sync but usb is async, it keeps sending wait / not ready to the sdcard host until usb command returns.

### slice manager

slice manager receives mmc commands over usb in a userspace daemon.
it looks up the relevant block in a ceph blockstore and returns it.
