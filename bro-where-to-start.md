# Where to start: Bro

(1) For an academic introduction, read the original Bro paper:
* http://www.icir.org/vern/papers/bro-CN99.pdf

The core system architecture hasn't changed much over the years, so if you want
to know how the system works internally, this paper has the details.

(2) Go through workshop from 2011 and do all the exercises:
* https://www.bro.org/bro-workshop-2011/
Solutions exist as well.

(3) Try to solve the Cyber Challenge from April 2013: the official instructions
have been removed, so here's the scoop. First, download this PCAP trace:
* http://www.icir.org/matthias/tmp/cq-2013-04.pcap

Then run Bro on it and figure out what happened in the trace.
There exist various types of central web attacks (RFI XSS, CSRF,
SQL injection) hidden in there, and your goal is to reconstruct
the sequence of events. By the way, knowing the different types
of attacks is also important for the web admin. Some guiding
questions:

- What's the SSID and WPA2 password of the Wifi?
- What are Chuck's credentials? What's his account balance?
- What does the attacker try to do with the router?
- How does Lester get 0wned? How much $$$ does he lose?
- What types of CSRF do you find?
- What types of XSS do you find?
- What's the main bug in index.php?
- What are the password hashes and passwords on the server?

For more details on the web attacks, please consult this lecture:

* http://www.icir.org/vern/cs161-sp13/slides/2.21.DoS-WebAttacks.pdf
* http://www.icir.org/vern/cs161-sp13/slides/2.26.WebAttacks2.pdf
* http://www.icir.org/vern/cs161-sp13/slides/2.28.WebAttacks3.pdf
