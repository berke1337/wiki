# How to start learning about security

## Basics
* Setup a virtual machine with your favorite operating system. If you haven’t used Linux yet, the latest Ubuntu LTS is a good start: http://www.ubuntu.com/download/desktop
* Feel comfortable in a linux or windows shell
* Having one VM running Kali Linux (https://www.kali.org/) can be useful because it comes with a lot of useful tools, but is not necessary.
* This youtube channel has a great introduction to “hacking” and also has some very nice video “write-ups” of past CTFs so you can get a feel of what to expect: https://www.youtube.com/playlist?list=PLhixgUqwRTjxglIswKp9mpkfPNfHkzyeN
* have a look at our Hacksheet: https://github.com/berke1337/hacksheet

## Getting started
You can go through the materials of the class CS 161: Computer Security.
* http://www.icir.org/vern/cs161-sp13/
* http://www-inst.cs.berkeley.edu/~cs161/sp14/

A huge list of additional readings is available at http://dfir.org/?q=node/8/.
A good background in Networking is important. Classes:
* EE 122: http://www-inst.cs.berkeley.edu/~ee122
* CS 168: https://inst.eecs.berkeley.edu/~cs168/



## Hacking tutorials and Challenges

The [CyberQuests](http://uscc.cyberquests.org/) challenges happen on a monthly basis and involve various types of computer security puzzles.

The Youtube channel [liveoverflow](https://www.youtube.com/channel/UClcE-kVhqyiHCcjYwcpfj9w) has an awesome [series](https://www.youtube.com/watch?v=iyAyN3GFM7A&list=PLhixgUqwRTjxglIswKp9mpkfPNfHkzyeN) on reverse engineering and low-level exploitation.

https://exploit-exercises.com/ provides a variety of virtual machines, documentation and challenges that can be used to learn about a variety of computer security issues such as privilege escalation, vulnerability analysis, exploit development, debugging, reverse engineering, and general cyber security issues.

https://ctftime.org/ is a website that lists many CTF competition. There is one almost every weekend. Just participate! Don't now where to start? Search for CTF write-ups or have a look at liveoverflow.

PIVOT seems to have a challenge where you have extract data from network traffic and other
formats: http://pivotproject.org/challenges/digital-forensics-challenge and http://pivotproject.org/challenges/file-carving. Instead of Wireshark you can also use Bro.

__This Wiki__ provides several guides which you should have a look at.

## Network Intrusion Detection and Forensics
We have good experiences using Bro
* http://www.bro.org
* Bro Exercise: https://www.bro.org/community/exchange2013.html


## CCDC Resources
CCDC is the main competition BERKE1337 is competing in.
* National CCDC Preparation
   * http://blog.spiderlabs.com/2013/04/web-application-defenders-cookbook-ccdc-blue-team-cheatsheet.html
   * http://blog.strategiccyber.com/2013/04/24/national-ccdc-red-team-fair-and-balanced/
   * http://blog.strategiccyber.com/2012/10/04/dirty-red-team-tricks-ii-at-derbycon-2-0/
* CCDC
   * [Description of event from red team perspective](http://www.reddit.com/r/netsec/comments/17dfqf/red_teaming_a_ccdc_practice_event/)
   * [Finding malware with Sysinternals tools](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2012/SIA302)
   * [Hunting rootkits on Linux](http://cayfer.bilkent.edu.tr/~cayfer/linux/Detecting_and_Removing_Rootkits.html)


## Unix System Admin 1x1
For competitions like CCDC it is vital to be comfortable administering various services. As a challenge, pick a Linux distribution or a BSD you are not familiar with (how about CentOS or FreeBSD) and get the following services running:
* nginx webserver with PHP over fastcgi
* PostgreSQL and MySQL database
* Some web applications (e.g. Joomla, Wordpress, ...)
* Postfix Mailserver with virtual user management in MySQL
* Dovecot IMAP server
* TLS Certificates for HTTPS, SMTPS, IMAPS
* Apache with mod_security as reverse proxy in front of nginx (you would probably not do this in production but see it as an exercise)
* Compile and install some of the software above from source

## Windows
First we're going to cover some of the most magnificent tools in the Windows sysadmin's arsenal, the Sysinternals suite. This a set of tools written by some Windows experts that give you an incredible level of access to a lot of low-level Windows APIs, which allow you to find malicious stuff really effectively. The best place to grab these tools is from http://live.sysinternals.com/tools/

As soon as you visit that URL, you'll notice that there are a lot of tools in the suite. Not all of them are particularly relevant to us, but there are a few that are essential. In particular: Process Explorer (like a more powerful task manager), Autoruns (like a more powerful msconfig), and TcpView (a netstat-like tool). When I was learning these, the best resource I used was a video by the main creator, Mark Russinovich, about how to use them to manually fight malware. The latest version of that talk is available here: https://www.youtube.com/watch?v=80vfTA9LrBM. Yes, it's 90 minutes of lecture--but, I promise it'll be helpful.

Malware removal isn't the main point of CCDC--but there are notable similarities. The red team will be trying to run malicious processes on our machines, install persistence mechanisms to keep our boxes infected after reboots, and make suspicious network connections back to their command & control hosts.

So, as your first task, watch the video and play around with the tools mentioned therein. If you have a Windows system, you'll get a much better idea of what's running on it. If you have no access to a Windows box to try these on, let me know--I can probably arrange something for you.
