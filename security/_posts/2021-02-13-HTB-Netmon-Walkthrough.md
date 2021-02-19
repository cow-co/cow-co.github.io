---
layout: post
title: HTB Netmon Walkthrough
categories: security
---

## Summary

The next box in catchups-month is "Netmon", another easy box. In this box, we see the impact of public access to filesystems. Without further ado, let's hop to it!

## External Reconnaisance

### NMap Port Scan

We begin with our standard pair of NMap scans:

`sudo nmap -v -sC -sS -oN nmap-10-10-10-152-scripted.nmap 10.10.10.152`,

`nmap -v -p- -oN nmap-10-10-10-152-full.nmap 10.10.10.152`

These scans show the following open ports:

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



## Exploitation



## Privilege Escalation



## Conclusion


