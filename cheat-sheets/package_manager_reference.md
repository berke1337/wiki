# Package Managers Reference Configurations

### Debian - apt
default /etc/apt/sources.list:

#### Debian 8 Jessie (April 2015)
```
deb http://ftp.us.debian.org/debian jessie main
deb-src http://ftp.us.debian.org/debian jessie main

deb http://ftp.us.debian.org/debian jessie-updates main
deb-src http://ftp.us.debian.org/debian jessie-updates main

deb http://security.debian.org/ jessie/updates main
deb-src http://security.debian.org/ jessie/updates main
```

For Debian 7.0 Wheezy (May 2013) or Debian 6.0 Squeeze (February 2011) or even
earlier versions, just replace `jessie` with the correct codeword.


### Ubuntu - apt
sources.list generator under https://repogen.simplylinux.ch/

#### Ubuntu Trusty 14.04 LTS
```
###### Ubuntu Main Repos
deb http://us.archive.ubuntu.com/ubuntu/ trusty main restricted universe
deb-src http://us.archive.ubuntu.com/ubuntu/ trusty main restricted universe

###### Ubuntu Update Repos
deb http://us.archive.ubuntu.com/ubuntu/ trusty-security main restricted universe
deb-src http://us.archive.ubuntu.com/ubuntu/ trusty-security main restricted universe
```

Add missing public key: `apt-key adv --keyserver keyserver.ubuntu.com --recv-keys KEY_ID` KEY_ID should look like 2EA8F35793D8809A.

### Centos - yum
Example /etc/yum.repos.d/CentOS-Base.repo:

```
# Change gpgcheck to 0 if the keys have also been "optimized" off the system
[base]
name=CentOS-$releasever - Base
mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os
#baseurl=http://mirror.centos.org/centos/$releasever/os/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

# Released updates
[updates]
name=CentOS-$releasever - Updates
mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates
#baseurl=http://mirror.centos.org/centos/$releasever/updates/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6

# Additional packages that may be useful
[extras]
name=CentOS-$releasever - Extras
mirrorlist=http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras
#baseurl=http://mirror.centos.org/centos/$releasever/extras/$basearch/
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6
```
