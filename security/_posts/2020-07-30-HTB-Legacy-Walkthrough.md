---
layout: post
title: HackTheBox Legacy Walkthrough
tags: security htb ctf
---

## Summary

Legacy is a very easy box, good for an introduction to CTFs and hacking in general. It makes use of a classic Windows vulnerability, and just requires some very basic reconnaisance and exploitation skills. So with that in mind, this will be a very short walkthrough. Let's get to it!

## External Reconnaisance

As always, we start with some reconnaisance, namely using NMap. We kick off two separate scans, a more limited script scan across the 1000 most common ports, and a full non-scripted scan across all 65535 ports:

`sudo nmap -v -sC -sS -oX nmap-10-10-10-4-scripted.xml 10.10.10.4`

`nmap -v -p- -oX nmap-10-10-10-4-full.xml 10.10.10.4`

This reveals a simple Windows setup; running some SMB services (ports 139, 445), on what looks to be Windows XP (or an equivalent Windows Server version).

## Exploitation

Let's have a look for an exploit, see if there's one applicable to this version of Windows. We'll want to exploit the SMB service, since that seems to be the only externally-facing service currently running on the box.

A little searching on Google (or via Metasploit's search functionality) reveals a remote code execution (RCE) vulnerability in that version of Windows SMB: MS08-067.

We can use this exploit via Metasploit, set the `RHOSTS` variable to `10.10.10.4`, and `run` it. This opens up a Meterpreter shell for us. `getuid` shows we are running as `SYSTEM` already, so we don't even need to do any privilege escalation!

Now all we need to do is go to the Administrator and user (john) desktops to grab their flags, and that's it. Legacy pwnd!

## Conclusion

Hopefully this has been useful to help ease you into the core workflow for HackTheBox boxes (and indeed any sort of penetration testing really): reconnaisance --> exploit (optionally cleanup after this, but let's not worry about that right now). This flow keeps going as you progress through the engagement. If this were a real engagement, we'd conduct internal reconnaisance after the MS08-067 exploit, to see where key documents are being held, see what (if any) internal services we might be able to access, see if we can gain persistence if necessary, and so on.
