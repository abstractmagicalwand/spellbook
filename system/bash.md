# Bash

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
