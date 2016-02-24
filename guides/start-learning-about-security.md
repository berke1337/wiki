# How to start learning about security

## Basics
There are some fundamental basics you have to know to get started.
* Know what a virtual machine (VM) is. Install your favorite operating system inside a VM. If you haven't had any exposure to Linux yet, the latest Ubuntu LTS is a good start.
* Feel comfortable in a linux or windows shell
* ...

## Hacking tutorials and Challenges

The [CyberQuests](http://uscc.cyberquests.org/) challenges happen on a monthly basis and involve various types of computer security puzzles.

The Youtube channel [liveoverflow](https://www.youtube.com/channel/UClcE-kVhqyiHCcjYwcpfj9w) has an awesome [series](https://www.youtube.com/watch?v=iyAyN3GFM7A&list=PLhixgUqwRTjxglIswKp9mpkfPNfHkzyeN) on reverse engineering and low-level exploitation.

https://exploit-exercises.com/ provides a variety of virtual machines, documentation and challenges that can be used to learn about a variety of computer security issues such as privilege escalation, vulnerability analysis, exploit development, debugging, reverse engineering, and general cyber security issues.

https://ctftime.org/ is a website that lists many CTF competition. There is one almost every weekend. Just participate! Don't now where to start? Search for CTF write-ups or have a look at liveoverflow.

__This Wiki__ provides several guides which you should have a look at.


## Random External Resources
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
