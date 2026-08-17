# Hardware Documentation

## Summary
- HPZ420 Workstation - Intel Xeon E5-1620 - Quadro K2000 (Running Ubuntu Server)
- Main OS is installed on 120GB Internal 2.5" SSD
- 2 Internal Hard Disk Drives in a Raid 1 Configuration for redundancy
- Both are segate 1b hard drives connected via sata and securely mounted in drive bay
- Raid setup was configured using Ubuntu Server setup and is managed automatically by system

## Storage Layout
- **sda**      8:0    0 119.2G  0 disk\
├─sda1   8:1    0     1G  0 part  /boot/efi\
└─sda2   8:2    0 118.2G  0 part  /
- **sdb**      8:16   0 931.5G  0 disk\
└─md0    9:0    0 931.4G  0 raid1 /mnt/data
- **sdc**      8:32   0 931.5G  0 disk  
└─md0    9:0    0 931.4G  0 raid1 /mnt/data

## External Hardware
- Wired ethernet to 2.5GBe TP Link 8 port unmanaged switch
- One wired connection to Server and one wired connection to Personal Computer
- Allows for fast communication and transfer speeds between server and my main computer

**All main and important storage is kept inside /mnt/data which is part of the RAID configuration**

## Future Hardware Plans
- Configure ISP router to bridge mode and pass router responsibilities to personal router to handle DHCP, DNS and Ports
- Connect Access Point for wireless connectivity
- Add a UPS Power Backup to Server PC for protection during possible outages
