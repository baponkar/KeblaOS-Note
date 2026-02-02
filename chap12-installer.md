# How could anyone install a OS in a raw Disk?

A raw disk store raw data in different location . 
In this note my target is to make a installer program which would make a bootable disk and copy necessary files and directories in target disk.
The raw disk can be recognized by Sectors whic 512 byte size.

The following table depicts the contents of specified Sectors.Which have UEFI boot code:

.-----------.---------------------------------------.
| Sector no | Contents                              |
|-----------|---------------------------------------|
| 0         | Protective MBR                        |
| 1         | GPT Header                            |
| 2         | First Four GPT Entries                |
| ..        | ..                                    |
| 33        | Last Four GPT Entries                 |
| 34        | 0                                     |    => First Usable sector
| ..        | ..                                    |
| 2047      | 0                                     |
| 2048      | BPB SECTOR                            |    => Start of FAT32 FS (1MB Aligen), First Partition i.e. Boot Partition
| 2049      | FSInfo                                |
| 2050      | FAT, FAT                              |
| ..        |   | /                                 |
| ..        |   ├── boot.cat                        |
| ..        |   │                                   |
| ..        |   ├── boot/                           |
| ..        |   │   ├── kernel.bin                  |
| ..        |   │   ├── limine.conf                 |
| ..        |   │   ├── user_main.elf               |
| ..        |   │   ├── boot_loader_wallpaper.bmp   |
| ..        |   │   │                               |
| ..        |   │   └── limine/                     |
| ..        |   │       ├── limine_bios_cd.bin      |
| ..        |   │       ├── limine_bios_hdd.sys     |
| ..        |   │       └── limine_uefi_cd.bin      |
| ..        |   │                                   |
| ..        |   └── efi/                            |
| ..        |       └── boot/                       |
| ..        |           └── bootx64.efi             |
| ..        | ..                                    |    => End of FAT32 FS (100 MB is Sufficient)
| ..        | Something                             |    => Start of Second Partition
| ..        | ..                                    |
| ..        | Something                             |    => End of Second Partition
| n - 32    |  ..                                   |    => Last Usable Sector
| n - 33    |  First Four backup GPT Entries        |
| ..        |  ..                                   |
| n - 2     |  Last Four Backup GPT Entries         |
| n -1      |  Backup GPT Header                    |     => n = Total Sectors
|-----------|---------------------------------------|

