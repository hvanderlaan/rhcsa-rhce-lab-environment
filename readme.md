# RHCSA/RHCE Lab Environment
This is a study environment for studying your ex200/ex300 (rhcsa7/rhce7) certification. This study environment is created with [vagrant](https://www.vagrantup.com/) and [virtualbox](https://www.virtualbox.org/). Also the base os is a [ubuntu](https://www.ubuntu.com/) system and is tested on a [macOS Sierra](https://www.apple.com) system. But this environment should also work on other linux operating systems (prosible with some small alterations).

## Requirements
if you want to use this study environment you need to install some packages in order to create it.
```
- virtualbox >= 5.1.14
- vagrant >= 1.9.1
- pip >= 9.0.1
- ansible >= 2.2.1.0
```

## User information
| user name | password | server          |
|-----------|----------|-----------------|
| user      | ratencot | labipa          |
| root      | ratencot | labipa          |
| admin     | password | freeipa account |
| user      | ratencot | system1         |
| root      | ratencot | system1         |
| user      | ratencot | system2         |
| root      | ratencot | system2         |

## Build time
Build time on a MacBook Air is: `vagrant up  140,16s user 47,86s system 17% cpu 17:31,12 total`

This could be faster if you upgrade labipa server before you start. You could give the labipa server 2048MB of memory and 2 cpu's. The current configuration is 1024MB and 1 cpu. This should be sufficient for normal usage.

## Usage
```bash
$ vagrant up
# ssh via vagrant
$ vagrant ssh <labipa|system1|system2>
# ssh directly labipa
$ ssh 172.16.20.2 -l root
# ssh directly system1
$ ssh 172.16.20.10 -l root
# ssh directly system2
$ ssh 172.16.20.20 -l root
```
## RHCSA7 Objectives
* Understand and use essential tools
  * Access a shell prompt and issue commands with correct syntax
  * Use input-output redirection (>, >>, |, 2>, etc.)
  * Use grep and regular expressions to analyze text
  * Access remote systems using ssh
  * Log in and switch users in multiuser targets
  * Archive, compress, unpack, and uncompress files using tar, star, gzip, and bzip2
  * Create and edit text files
  * Create, delete, copy, and move files and directories
  * Create hard and soft links
  * List, set, and change standard ugo/rwx permissions
  * Locate, read, and use system documentation including man, info, and files in /usr/share/doc
* Operate running systems
  * Boot, reboot, and shut down a system normally
  * Boot systems into different targets manually
  * Interrupt the boot process in order to gain access to a system
  * Identify CPU/memory intensive processes, adjust process priority with renice, and kill processes
  * Locate and interpret system log files and journals
  * Access a virtual machine's console
  * Start and stop virtual machines
  * Start, stop, and check the status of network services
  * Securely transfer files between systems
* Configure local storage
  * List, create, delete partitions on MBR and GPT disks
  * Create and remove physical volumes, assign physical volumes to volume groups, and create and delete logical volumes
  * Configure systems to mount file systems at boot by Universally Unique ID (UUID) or label
  * Add new partitions and logical volumes, and swap to a system non-destructively
* Create and configure file systems
  * Create, mount, unmount, and use vfat, ext4, and xfs file systems
  * Mount and unmount CIFS and NFS network file systems
  * Extend existing logical volumes
  * Create and configure set-GID directories for collaboration
  * Create and manage Access Control Lists (ACLs)
  * Diagnose and correct file permission problems
* Deploy, configure, and maintain systems
  * Configure networking and hostname resolution statically or dynamically
  * Schedule tasks using at and cron
  * Start and stop services and configure services to start automatically at boot
  * Configure systems to boot into a specific target automatically
  * Install Red Hat Enterprise Linux automatically using Kickstart
  * Configure a physical machine to host virtual guests
  * Install Red Hat Enterprise Linux systems as virtual guests
  * Configure systems to launch virtual machines at boot
  * Configure network services to start automatically at boot
  * Configure a system to use time services
  * Install and update software packages from Red Hat Network, a remote repository, or from the local file system
  * Update the kernel package appropriately to ensure a bootable system
  * Modify the system bootloader
* Manage users and groups
  * Create, delete, and modify local user accounts
  * Change passwords and adjust password aging for local user accounts
  * Create, delete, and modify local groups and group memberships
  * Configure a system to use an existing authentication service for user and group information
* Manage security
  * Configure firewall settings using firewall-config, firewall-cmd, or iptables
  * Configure key-based authentication for SSH
  * Set enforcing and permissive modes for SELinux
  * List and identify SELinux file and process context
  * Restore default file contexts
  * Use boolean settings to modify system SELinux settings
  * Diagnose and address routine SELinux policy violations

## RHCE7 Objectives
* add a repository to yum (location is provided in exam)
* create a bond with ipv4 or ipv6 address
* create a team with ipv4 or ipv6 address
* configure ssh
    * deny/allow users (tip: service configuration)
    * deny/allow networks (tip: tcpwrappers)
* configuration portforwarding (firewalld and rich rules)
* configure your system as router (tip: sysctl.d/forward.conf and net.ipv4.ip_forward)
* configure iSCSI SAN (non chap) (tip: targetcli)
* configure iSCSI initiator (tip: iscsiadm)
* configure NFS server
* configure NFS server (secure: krb5 <-- real pain in the ass differs on 7.0, 7.1, 7,2)
* configure SMB server
* configure SMB server (multi user)
* configure file-based storage with SMB
* installing mariadb (tip: firewalld)
* create simple database
* mariadb backup / restore (tip: mysqldump)
* mariadb querying (inner joins, you know the drill)
* configure cachonly DNS server (tip: unbound)
* configure email delivery (tip: Null-Client should be enough, extra tip: postconf command 10x)
* installing apache/httpd (tip: firewalld, selinux)
* configure vhost with ssl redirect (tip: mod-rewrite)
* configure dynamic web content (tip: firewalld, SELINUX !!!!!!!)
* configure confedential webpage (restiction done by apache, could diff between apache 2.2 and 2.4)
* bash scripting

## Todo
- [x] Fix network [issues #1](https://github.com/hvanderlaan/rhcsa-rhce-lab-environment/issues/1) system1 and system2
- [x] Add RHCSA Objectives
- [x] Dns resolving done by labipa server
- [ ] Create reccors in labipa dns for system1 and system1
- [ ] Make ansible playbooks idempotent
- [ ] Add 2 extra interfaces for link aggregation (RHCE7)

## Legal notice
If you are searching for answers or spoilers to the EX300K / RHCE7 exam, this is not the place to search. This is only a tool to study. Also you should study for this exam, you will never learn it when you only learn the answers.

## License
rhcsa-rhce-lab-environment is licensed under the GPLv3:
```
This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.

For the full license, see the LICENSE file.
```
