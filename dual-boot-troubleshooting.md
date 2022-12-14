## Windows 11 - Ubuntu Dual boot notes:

### Removing Ubuntu and GRUB
- delete the ubuntu partition
- go to disk management and remove the partition
- this will mess up booting to windows

#### Checking Boot Partition
- to see the boot partition from windows open an admin cmd
- run diskpart
```
C:\WINDOWS\system32>diskpart
```
- see disks on system. see how gpt and mbr can be identified here. * for gpt, no star for mbr
```
DISKPART> list disk

  Disk ###  Status         Size     Free     Dyn  Gpt
  --------  -------------  -------  -------  ---  ---
  Disk 0    Online          465 GB      0 B        *
```
- pick the disk with windows. the boot/efi partition should be on the disk.
```
DISKPART> sel disk 0

Disk 0 is now the selected disk.
```
- see the partitions on the disk. select the boot partition. the right partition will be a system partition. it won't have a drive letter. the file system of this system partition will be FAT32.
```
DISKPART> list vol

  Volume ###  Ltr  Label        Fs     Type        Size     Status     Info
  ----------  ---  -----------  -----  ----------  -------  ---------  --------
  Volume 0     E                       DVD-ROM         0 B  No Media
  Volume 1     C   Windows      NTFS   Partition    445 GB  Healthy    Boot
  Volume 2     D   RECOVERY     NTFS   Partition     18 GB  Healthy
  Volume 3         Windows RE   NTFS   Partition    980 MB  Healthy    Hidden
  Volume 4                      FAT32  Partition    260 MB  Healthy    System
  Volume 5                      NTFS   Partition    540 MB  Healthy    Hidden

DISKPART> sel vol 4

Volume 4 is the selected volume.
```
- give the boot partition a letter so it can be browsed with DIR. repeat list vol to see the result.
```
DISKPART> assign letter=p

DiskPart successfully assigned the drive letter or mount point.

DISKPART> list vol

  Volume ###  Ltr  Label        Fs     Type        Size     Status     Info
  ----------  ---  -----------  -----  ----------  -------  ---------  --------
  Volume 0     E                       DVD-ROM         0 B  No Media
  Volume 1     C   Windows      NTFS   Partition    445 GB  Healthy    Boot
  Volume 2     D   RECOVERY     NTFS   Partition     18 GB  Healthy
  Volume 3         Windows RE   NTFS   Partition    980 MB  Healthy    Hidden
* Volume 4     P                FAT32  Partition    260 MB  Healthy    System
  Volume 5                      NTFS   Partition    540 MB  Healthy    Hidden
```
- exit diskpart
```
DISKPART> exit

Leaving DiskPart...
```
- directly use the dir command, don't cd into the partition first.
```
C:\WINDOWS\system32>dir p:
 Volume in drive P has no label.

 Directory of P:\

16-10-2020  11:26    <DIR>          EFI
               0 File(s)              0 bytes
               1 Dir(s)     177,442,816 bytes free

```
- EFI will have boot files for all operating systems. Microsoft directory has stuff for windows boot manager. ubuntu directory has stuff for ubuntu.
- delete the ubuntu directory which contains grub using `rm ...` or `rmdir ...`.





### TODO
- write comments for these useful commands
```
from GRUB RESCUE
insmod part_gpt
insmod chain
set root=(hd0,gpt1)
chainloader \EFI\Microsoft\Boot\bootmgfw.efi
boot
```

- look up - recovery admin cmd commands
```
bcdedit
bootrec
bootcfg
bootrec /rebuildbcd
###
bcdbood c:/windows
###
```

- please don't run these sort of commands unless you know what you are doing.
```
bcdedit /deletevalue {bootmgr} ...
```

### How to create a windows recovery drive
- windows button
- search create recovery drive
- tick `back up system files to the recovery drive`
- insert flash drive > 16gb
- next/continue to the end
