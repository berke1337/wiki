# Windows Incidents Reports

### Meterpreter
Metasploit Meterpreter injects itself as a DLL in to a target process, and then
starts a new thread in that process that runs that DLL. This allows it to stay
off disk and without an easily-spotted process name. There are some things that
you can do to help find it though:

The thread it uses tends to have a high "CSwitch Delta" count, even when idle.
(Go to a process' properties in Process Explorer and then go to the Threads tab
to see this). In testing, it was usually around 65, which is a lot higher than
most service threads. This number represents how many context switches the
thread goes through.

### Cobalt Strike
Cobalt Strike uses the Metasploit Framework and the Meterpreter for a lot of its
functionality, so a much of the above applies here as well. There are a few
additional things to note:

* Defaultly Cobalt Strike uses notepad.exe to migrate in to. Keep a very close
  eye on notepad processes in your system.
* Cobalt Strike beacons can work through HTTP, DNS, or SMB. Firewall your box so
  that connections on these ports can only be made to the right places (the
  competition proxy for HTTP, the team DNS server for DNS, and probably only the
  domain controller for SMB). Caveat: Server 2003, XP, and below don't support
  outbound firewalling. You'll have to rely on the bastion being up for those
  boxes.
