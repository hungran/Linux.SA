# Linux.SA
 - Vũ Mạnh Hùng

# 20192509
 1. Booting and SMD
 2. FileSystem
 
## Booting and SMD
** Boot Process
  1. Find
  2. Load
  3. Running Bootstrapp code
  4. Running startup script -> system deamons
 
 <img src="https://imgur.com/XjpWlE0.jpg">
 
 *Note*:  
	'Before the system is fully booted, filesystems must be checked and mounted and system
daemons started. These procedures are managed by a series of shell scripts (sometimes called
“init scripts”) or unit files that are run in sequence by **init** or parsed by **systemd**.'

** System Firmware
 - Device on motherboard such as SATA, network interface, USB...
** BIOS vs UEFI std
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
	'**/efi/boot/bootx64.efi
	or on ubuntu
	'**/efi/ubuntu/grubx64.efi
	- show config boot
		'**efibootmgr -v**'
		