# limit-fs
FUSE filesystem that removes the oldest files whenever the free space
reaches the set percentage.

You can use it in a no empty directory, anything you write in will be
written in the underlying filesystem. After unmounting it all files
remain in the unmounted directory.

## How to use in Linux
Once limit-fs is installed running it is very simple:

```
limit-fs [FUSE options] [mount options] mountPoint
```
It is recommended to run limit-fs as regular user (not as root). For
this to work the mount point must be owned by the user.

To unmount the filesystem:
```
fusermount -u mountpoint
```

## File-system specific options

You can specify the options:

| option | default | description |
|:-:|:-:|---|
| --usage-limit=<d>  | 80 | set the usage limit in percentage. |

## Example
```
limit-fs --usage-limit=90 /mnt/
```

## How to use in BSD or macOS

On BSD and macOS, to unmount the filesystem:
```
umount mountpoint
```

## Installation from source
 1. Download source files:
    `git clone https://github.com/piuma/limit-fs.git` 
    
 2. 'cd' to the directory containing the package's source code and type
    './configure' to configure the package for your system.
    `cd limit-fs && ./configure`

 3. Type 'make' to compile the package.
    `make`

 4. Type 'make install' to install the programs and any data files and
    documentation.  When installing into a prefix owned by root, it is
    recommended that the package be configured and built as a regular
    user, and only the 'make install' phase executed with root
    privileges.
    `sudo make install`

### Manual compile
```
gcc -Wall limit-fs.c `pkg-config fuse3 --cflags --libs` -lulockmgr -o limit-fs
```