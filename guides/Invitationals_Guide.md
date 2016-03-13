# Invitationals Guide

CCDC Invitationals are a great place to get your feet wet with CCDC, network
defense, and security in general. They're low-stress, allow many people to
participate, and give a good feeling for what the real event is like. This page
will go through some of the things involved and how to best prepare for them.

## Scoring Although Invitational competitions don't affect our team's
qualification, there's still a scoring system in place, and it's basically the
same as the one at qualifiers and regionals. Your score comes from three
places:
* Uptime: how consistently the services your network has are functional. These
  services tend to be things like websites, mail servers, and DNS servers.
* Injects: "inject" is the word CCDC uses for "challenge" or "task." Injects
  are given throughout the course of the competition and ask the team to do a
  variety of things. These frequently involve setting up new services or
  changing existing ones. Injects have time limits, and presenting results is
  important.
* Defense: whenever one of your services or servers gets compromised by a
  member of the Red Team, you lose points. You can gain up to 50% of these
  points back by submitting a detailed incident report. Examples of information
  to include on an incident report would be attacker IP address(es), effect of
  the breach, and how the compromise is being dealt with or resolved.

## Things that are Important and Difficult Our team has done quite a few CCDC
competitions at this point. There are a few issues that we've had difficulties
with, and they're important to keep in mind.
* Communication: our basic competition plan centers around a Team Captain that
  is in charge of dispatching tasks and making sure people stay on track. It's
  easy to get stuck solving small technical problems for a long time, while
  losing sight of the big picture and letting the hackers in (or other similar
  disasters). It's critical to effectively communicate what you're working on
  and what you know to the Captain.
* Task Dispatch: sometimes you end up with too much to be working on at once.
  This is normal--there's a huge amount going on at CCDC. It's then extra
  important to make sure that someone helps you out, because it's not uncommon
  for at least one person on the team to be undertasked.
* Staying calm and focused: CCDC can get stressful and exciting, usually at the
  same time. It's critical to stay calm and keep going.

## What's going to happen at Invitationals
* Arrive 20 minutes before the competition starts. Bring a laptop that has Java
  installed and available as a web browser plugin. _(Yes, we know this is a bad
  security practice. It's the only way to work with their environment. Use a VM
  if you like.)_
* Find out who is currently acting as team captain and say hello. Make sure
  they know you're there to help and what you consider to be your strength (see
  Areas of Expertise below).
* The competition will start. The first step is always all about inventory. We
  need to find out what machines we're defending, what they're running, and how
  to keep them safe. In the beginning, split up in to a number of groups equal
  to the number of machines we're responsible for. Each group takes a machine
  and finds out everything they can about it. Results go on the whiteboard.
  Critical things to look for include:
   * What business services is it running?
   * Does it have a firewall? Has that firewall been configured to block
     everything except intended services?
   * What's the patch level of the machine? Windows XP? Windows Server 2012R2?
     Ubuntu 7.12?
* Injects will arrive quickly. The team captain will dispatch tasks.
* Soon you'll move in to the "general hardening" phase. This is when you take
  your assigned system and try and make it as resilient as possible. The place
  to go for this part is the [[Secure-Server-Checklist]].

## Areas of Expertise At invitationals you don't have to come in knowing
exactly what to do, or be a master at configuring or securing any particular
type of system. It's helpful, however, if you have some idea of what you're
best at (or what you're most interested in) in the following areas.
* *Management*. We've had huge success in the past having someone be Master of
  All Injects, and they dispatch them to other people and make sure they get in
  on time.
* *Windows defense*. Do you love domains? Script PowerShell for fun? Probably
  not, but if you're most familiar with windows we can use your skills.
* *Unix defense*. We always get a lot of Unix servers to protect. Knowing your
  way around a shell is a valuable thing.
* *Networking*. A good network structure is the base of our defense plan.
  Network fundamentals are very useful to know, as is info about how to
  configure switches and routers (specifically of the Cisco or Juniper
  varieties).
