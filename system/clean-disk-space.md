# Free up disk space

## Show size by disk

```sh
df -H
lsblk
```

## Show size swap

```sh
free
```

## Arch

```sh
sudo pacman -Sc
```

### Ubuntu and Debian

- [How do I free up disk space?](https://askubuntu.com/questions/5980/how-do-i-free-up-disk-space)
  - [Comment](https://askubuntu.com/a/6002)

Show top 10 biggest subdirs in the current dir:

```sh
du -sk * | sort -nr | head -10
```

```sh
apt-get autoclean
apt-get --purge autoremove
swapoff -a
swapon -a
rm /tmp/*
```
