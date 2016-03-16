# Linux and BSD quick start
Imagine you encounter a operating system you have never used before or heard of
before. This cheat sheet should give you the most important information about
the OS at hand.

## TODO

This document is under construction. Please improve it.  At the end we want to
have:

For standard Linuxes and BSDs
* how to find out version
* where to configure repository information
* standard package manager commands
* installed packages
* update repository
* install/upgrade 1 package
* search for a package
* firewalls

### Find out what box you are sitting in front of

```bash
cat /etc/*-release
lsb_release -a
cat /proc/version
```

### Filesystem Hierarchy Standard

https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard

## Linuxes

Linux            | Latest Release                           | Comments
-----------------|------------------------------------------|-----------------
Debian 		       | 8.3 - Jessie (January 23, 2016)          | Very stable linux, often used for servers. Uses apt as package manager.
Ubuntu     		   | 15.10 - Wily Werewolf (October 21, 2015) | Based on Debian
Mint		         | 17.3 - Rosa (January 9th, 2016)          | Similar to debian
RHEL             | 7.2, 6.7, 5.11 (November 19, 2015)       | Red Hat Enterprise Linux. Package manager: RPM. Update method: Yum / PackageKit
CentOS		       | 7.2-1511 (December 14th, 2015)           | Release numbers are based off RHEL, binary-compatible to RHEL
Scientific Linux |                                          | Binary-compatible to RHEL
Oracle Linux     |                                          | Binary-compatible to RHEL
Fedora		       | 23 (November 3rd, 2015)                  | See RHEL
SLES (SUSE)	     | 12SP1 (December 18, 2015)                | (SUSE Linux Enterprise Server) Package manager: RPM. Update method: Zypper/YaST2
Void Linux 	     | Rolling release                          | Entire new system
ArchLinux        |                                          |
Slackware        |                                          |
Mageia           |                                          | Update Method: urpmi (rpmdrake). Package manager: RPM
ClearOS          |                                          |
Gentoo           |                                          |


## BSDs
BSD           | Comments
--------------| -------------
FreeBSD		    | by far most popular BSD. Latest version is 10.2 (2015-08-13)
OpenBSD		    | Latest version: 5.8 (2015-10-18)
NetBSD		    | Latest version: 7.0 (2015-10-08)
Darwin		    | Latest version: 15.0.0 (2015-09-16), released by Apple. OX X is based on Darwin. Package manager: No standard. There are ports available for MacPorts (formerly DarwinPorts), Fink, Homebrew, RPM, pkgsrc, and Portage
DragonFly BSD | Based on FreeBSD, Latest version: 4.0.3 (2015-01-21). Package manager: pkgng


## Package Managers

Manager | Info
--------|------------
RPM     | There are binary rpms (BRPMs) and source rpms (SRPMs), indicated by “.src.rpm”
yum     | Used for RHEL, CentOS, Fedora, etc. Uses .rpm packages
pacman  | Package manager for Arch, lots of community support online
dpkg    | Debian-based package installer (.deb packages) `dpkg -i <package>` installs a package, `dpkg -L <package>` shows files installed by a package
APT     | Pretty much just a front-end for `dpkg` over the network
portage | Gentoo package manager, uses `emerge` behind the scenes


## Update Methods

Update Method | Info
--------------|----------
apt-get       | Uses dpkg as backend. See https://wiki.archlinux.org/index.php/Pacman/Rosetta and https://help.ubuntu.com/community/AptGet/Howto
pacman        | See https://wiki.archlinux.org/index.php/Pacman/Rosetta
dnf           | See https://wiki.archlinux.org/index.php/Pacman/Rosetta
zypper        | See https://wiki.archlinux.org/index.php/Pacman/Rosetta
emerge        | See https://wiki.archlinux.org/index.php/Pacman/Rosetta
xbps          | See https://wiki.archlinux.org/index.php/Pacman/Rosetta
urpmi         | x
YaST2         | x
yum           | Uses rpm as backend
