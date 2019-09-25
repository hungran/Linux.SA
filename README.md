# Linux.SA
 - Vũ Mạnh Hùng

# 20192509
 1. Booting and SMD
 2. FileSystem
 
# 1.Booting and SMD
## Boot Process Overview
  1. Find
  2. Load
  3. Running Bootstrapp code
  4. Running startup script -> system deamons
 
 <img src="https://imgur.com/XjpWlE0.jpg">
 
 *Note*:  
	'Before the system is fully booted, filesystems must be checked and mounted and system
daemons started. These procedures are managed by a series of shell scripts (sometimes called
“init scripts”) or unit files that are run in sequence by **init** or parsed by **systemd**.'

## 1.2 System Firmware
	- Device on motherboard such as SATA, network interface, USB...
## 1.3 BIOS vs UEFI std
 1. BIOS (Basic In / Out System)
	- Traditional PC firmware
	- BIOS relate Legacy BIOS
	- Boot with device starts with MBR (Master Boot Record)
 2. UEFI (or reversion of EFI)
	- use GPT disk partition (GUID Parition Table)
	- use FAT filesystems
	- use EFI System Part (ESP) at boot time
	- ESP available be mounted, read, written maintain by OS
	Note: *Not to run MBR-specific admin tool on GPT disk because BIOS system can't see the full GPT part table.
	- normal path
	`/efi/boot/bootx64.efi`
	or on ubuntu
	`/efi/ubuntu/grubx64.efi`
	- show config boot
	`efibootmgr -v`
## 1.4 Boot Loader
 - eg: GRUB
## 1.5 GRUB (Grand unified boot loader)
 - Original GRUB: GRUB Legacy
 - Extra-crispy GRUB 2 is **current standard** (for Ubuntu and RHEL)
 - Available to boot FreeBSD (UNIX) 
 - Stored system's NVRAM
 - It came from regular text file **grub.cfg**.
 Path 
 `/boot/grub` 
 or in RHEL and CentOS
 `/boot/grub2`
 - Available to create by yourself
 - Path
 `/etc/default/grub`
 - Modify or configure by **grub2-mkconfig**
 -GRUB config options **/etc/default/grub`
 |shell var| Contents or function |
 |-------------------|----------------------|
 |GRUB_BACKGROUND| Background image **must be .png, .tga, .jpg or .jpeg file**
 |GRUB_CMDLINE_LINUX| Kernel parameters to add |
 |GRUB_DEFAULT| Number or title of the menu entry|
 |GRUB_DISABLE_RECOVERY| Prevent the generation of recovery mode entries|
 |GRUB_PRELOAD_MODULES| List of GRUB modules to be loaded as early as possible|
 |GRUB_TIMEOUT| Second to display the boot menu before autoboot|