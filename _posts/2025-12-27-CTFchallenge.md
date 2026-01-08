---
layout: post
title: CTF Reversing Engineering Challenge
---

![_config.yml]({{ site.baseurl }}/images/diaTitle.png)

## Cyberpsychosis Challenge from Hack The Box 

I have been really enjoying the reverse engineering challenges from HTB. I recently completed one that I found very interesting I will not post the name of the challenge or the flag to keep within HTB rules, but I wanted to do a write up as it involved a Linux root kit which is something I have not previously analysed.

### Challenge Scenario
Malicious actors have infiltrated our systems and we believe they've implanted a custom rootkit. Can you disarm the rootkit and find the hidden data?

#### File Command
I always start by running the file command on a binary to get as much infromation as possible about what I am looking at:
![_config.yml]({{ site.baseurl }}/images/filecommand.png)

