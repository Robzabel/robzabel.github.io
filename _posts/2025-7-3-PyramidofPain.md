---
layout: post
title: The Pyramid of Pain
---

![_config.yml]({{ site.baseurl }}/images/Pyramid.png)

Not all indicators of compromise (IoCs) are equal. It’s crucial to understand the relative value of different types of IoC and use them appropriately in the threat intelligence process. The Pyramid of Pain is a conceptual model that classifies and prioritises IoCs based on their effectiveness in detecting threats

The pyramid is a visual representation of the amount of pain defenders cause a malicious actor by denying them certain indicators or working to disrupt their operations. At the bottom of the pyramid are the easiest defensive maneuvers an attacker can get around, while the top represents the hardest to circumvent.

## Tactics, Techniques and Procedures (TTPs)

TTPs are behavioural patterns that make up an attackers working methodologies. These methods can be learned by profiling an attacker and responding accordingly. For example if an attacker is sending their malware in PDF attachments in emails, filtering all emails containing PDF files will force them to rethink their initial access technique.

## Tools

Identifying the tools an attacker is prone to using is vital for defenders. It is easy to mitigate known nefarious tools such as metasploit, but if an attacker is using "live of the land" binaries (LOLBins) to carry out thier objectives it becomes dificult to block. Defenders will need intelligence to create monitoring and detection rules for when these legitimate applications are abused in an environment.

## Network/Host Artifacts

This can be as simple as changing where directories are commonly created in file systems or defining specific registry values that should not be changed on a PC. Networks can be segregated into VLANS and network devices such as routers/switches can be changed from the convetional IP addresses such as a .1 or .254, to a random number.

## Domain Names

Domain names can be easily blocked on firewalls; however the proocess of changing domain name is simple and an attacker can rapidly alter the DNS of their infrastructure to circumvent any blocklists.

## IP Addresses 

IP addresses can produce false positives for defenders as data centres and content delivery networks NAT public IP addresses. This allows attackers to appear to come from legitimate source locations. Changing IP address is also trivail as a VPN, SOCKS Proxy chain and TOR can all be used to mask an IP address.

## Hash Values

File hashes can be completely changed by simply adding or removing a single character. Therefore, hash values is at the bottom of the pyramid.