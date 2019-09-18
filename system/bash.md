# Bash

[A guide to learn bash](https://github.com/Idnan/bash-guide)

## Show running processes

```sh
ps aux
top
htop
```

## Check which Linux distro

```sh
cat /etc/issue
```

## Check the current permissions on a file

```sh
ls -l linkextractor.py
```

## Change permission

`-rw-r--r--` indicates that the script is not set to be executable. We can change it by
running `chmod a+x script.py`.

## Replace all occurrences

```sh
sed -i 's/Link Extractor/Super Link Extractor/g' www/index.php
```

## How to copy the content of a folder to another existing folder

```sh
cp -a /public/. /dist/
```

The `-a` option is an improved recursive option, that preserve all file attributes, and also preserve
symlinks.

The `.` at end of the source path is a specific `cp` syntax that allow to copy all files and folders,
included hidden ones.
