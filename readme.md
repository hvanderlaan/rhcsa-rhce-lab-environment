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
| user name | password | server  |
|-----------|----------|---------|
| user      | ratencot | labipa  |
| root      | ratencot | labipa  |
| user      | ratencot | system1 |
| root      | ratencot | system1 |
| user      | ratencot | system2 |
| root      | ratencot | system2 |

## Build time
Build time on a MacBook Air is: `vagrant up  140,16s user 47,86s system 17% cpu 17:31,12 total`

This could be faster is you upgrade labipa server before you start. You could give the labipa server 2048MB of memory and 2 cpu's. The current configuration is 1024MB and 1 cpu. This should be sufficient for normal usage.

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
- [ ] Create custom hosts files for system1 and system2
- [ ] Make ansible playbooks idempotent
- [ ] Add 2 extra interfaces for link aggregation (RHCE7)
- [ ] Add RHCSA Objectives

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
