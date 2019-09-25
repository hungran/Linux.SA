# Linux.SA
 - Vũ Mạnh Hùng

# 20192509
 1. Booting and SMD
 2. FileSystem
 
## Booting and SMD
 ** Boot Process **
  1. Find
  2. Load
  3. Running Bootstrapp code
  4. Running startup script -> system deamons
 
 <img src="https://imgur.com/XjpWlE0.jpg">
 
 *Note*:  Before the system is fully booted, filesystems must be checked and mounted and system
daemons started. These procedures are managed by a series of shell scripts (sometimes called
“init scripts”) or unit files that are run in sequence by *init* or parsed by *systemd*.
