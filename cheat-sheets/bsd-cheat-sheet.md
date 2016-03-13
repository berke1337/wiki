# BSD Cheat Sheet

### Explore the system, see what is running

* `sockstat` -- lists open sockets
* `tail -f -n 30 /var/log/syslog` monitor log

### General BSD hints
* The group wheel allows you to su (and maybe other stuff)
* For package management there are two ways: ports (installing from source) and
  packages (installing binaries). Both understand dependencies
* The package manager is `pkg`
* `pkg search`, `pkg update`, `pkg upgrade`, as usual, `pkg delete` for
  uninstall  
* repos configured under `/usr/local/etc/pkg/repos/`. Default repo can be
  disabled by creating `FreeBSD.conf` with content `FreeBSD: {enabled: no}`
* startup configuration is `/etc/rc.conf`
* config files are in `/usr/local/etc/`
* undeletable flag: `chflags sunlink file1`, `chflags nosunlink file1`. View
  flags: `ls -lo file1`
* change to bash (permanently) `chsh -s /usr/local/bin/bash`
* set http proxy `setenv HTTP_PROXY http://ProxyNameOrIp:8080`
* network config file: `/etc/rc.conf`.

### rc.conf

```
hostname="new.host.name"
```

### Package Management
There is `pkg` for managing pre-compiled packages and ports for compiling from
source.
* Download the official ports collection: `portsnap fetch; portsnap extract`
* To update, use `portsnap fetch update`
* To install a port: `cd /usr/ports/yourArea/yourPackage` and `make install`.
  Can also do `make deinstall`.
