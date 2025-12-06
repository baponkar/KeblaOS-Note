# How could anyone install a OS in a raw Disk?

A raw disk store raw data in different location . 
In this note my target is to make a installer program which would make a bootable disk and copy necessary files and directories in target disk.
The raw disk can be recognized by Sectors whic 512 byte size.

The following table depicts the contents of specified Sectors.Which have UEFI boot code:

| Sector no | Contents                         |
|-----------|----------------------------------|
| 0         | Protective MBR [0-445:boot code]                                 |
| 1         |                                  |