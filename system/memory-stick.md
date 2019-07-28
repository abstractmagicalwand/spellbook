# Memory Stick

## Formatting

```sh
fdisk -l
umount /dev/sdb

fsck.vfat -f -p /dev/sdb
# or
mkfs.vfat -n 'name_for_your_pendrive' -I /dev/sdb1
```

## Burn

`sudo dd bs=4M if=[ur .iso] of=/dev/sd[that 1 letter] status=progress`
