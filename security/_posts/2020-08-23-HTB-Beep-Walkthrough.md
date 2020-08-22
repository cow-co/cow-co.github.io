---
layout: post
title: HTB Beep Walkthrough
categories: security
---

## Summary

Beep is another easy box, focusing again on simple searching for published exploits. However, unlike [Legacy]({% post_url 2020-07-30-HTB-Legacy-Walkthrough %}), there is more junk to sift through during the reconnaisance phase.

## External Reconnaisance

### NMap Port Scan

As always, we start with some NMap reconnaisance. We kick off two separate scans, a more limited script scan across the 1000 most common ports, and a full non-scripted scan across all 65535 ports:

`sudo nmap -v -sC -sS -oX nmap-10-10-10-7-scripted.xml 10.10.10.7`

`nmap -v -p- -oX nmap-10-10-10-7-full.xml 10.10.10.7`

We find the following ports are open:

| port      | state | service          |
| --------- | ----- | ---------------- |
| 22/tcp    | open  | ssh              |
| 25/tcp    | open  | smtp             |
| 80/tcp    | open  | http             |
| 110/tcp   | open  | pop3             |
| 111/tcp   | open  | rpcbind          |
| 143/tcp   | open  | imap             |
| 443/tcp   | open  | https            |
| 879/tcp   | open  | unknown          |
| 993/tcp   | open  | imaps            |
| 995/tcp   | open  | pop3s            |
| 3306/tcp  | open  | mysql            |
| 4190/tcp  | open  | sieve            |
| 4445/tcp  | open  | upnotifyp        |
| 4559/tcp  | open  | hylafax          |
| 5038/tcp  | open  | unknown          |
| 10000/tcp | open  | snet-sensor-mgmt |

This indicates we have some web server running, plus a SQL database and an email server. Interesting. In a real engagement, we might be particularly interested in the potential for staging a phishing campaign via the mail server.

### Web Reconnaisance

Let us take a look at that web service. A quick navigation to `https://10.10.10.7` shows a login page for something called "Elastix". We'll take note of that.

We then chuck DirBuster at it, using the 2.3-medium wordlist, and checking for `.php` extensions. Dirbuster starts spitting out a very large set of files and directories, but we needn't wait for it to finish. Fairly soon, we start seeing pages popping up for `/mail/index.php` ("Roundcube" mail) and `/admin/config.php` (FreePBX, which seems to be on version 2.8.1.4 when we navigate to it).

That should be enough to be getting on with, so let's have a look around for exploits.

## Exploitation

Elastix and FreePBX are our primary targets; the latter because it is an admin interface, and the former because it provides a login endpoint; if it's login-protected, then there's probably something juicy behind it. As mentioned above, in a real engagement we might prioritise the Roundcube mail server instead, depending on the scope of our engagement.

Two immediate candidates pop up for exploits: [one for Elastix](https://www.exploit-db.com/exploits/37637), and [one for FreePBX](https://www.exploit-db.com/exploits/41005). The former is verified, whereas the latter is not, so we'll go with the Elastix exploit for now.

The exploit seems to be a local file inclusion exploit against a URL parameter; seemingly related to how the server loads language/translation files. The exploit is simple; we just navigate to `https://10.10.10.7/vtigercrm/graph.php?current_language=../../../../../../../..//etc/amportal.conf%00&module=Accounts&action`.

What is returned seems to be a configuration file for FreePBX, interestingly. It's a large configuration file, but near the top we find some usernames and passwords. We note that all the passwords seem to be the same, so that gets us thinking: perhaps they've reused those passwords elsewhere? Perhaps for SSH logins?

We attempt to log in as `root`, using the password we've found, and voila! We're in.

[<img src="https://media.giphy.com/media/3knKct3fGqxhK/giphy.gif" alt="Create a new shell instance" style="width: 400px;"/>](https://media.giphy.com/media/3knKct3fGqxhK/giphy.gif)

## Conclusion

Another pretty easy one, this, but it's starting to ease you into more complex environments with more components to recon and to think about. I like to emphasise a breadth-first approach to pentesting: conducting broad reconnaisance across the system before diving into any one particular aspect. We'll see this come up more and more as we progress.
