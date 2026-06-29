---
layout: post
title: FortiBleed - Why This Campaign Is Far More Than a Simple Credentials Leak
---

![_config.yml]({{ site.baseurl }}/images/Titlefortibleed.png)

## Discovery   

At first glance, the FortiBleed campaign appeared to be yet another large-scale credentials leak affecting Fortinet firewalls. However, the reality is far more concerning. Rather than being centred around a single vulnerability or newly discovered exploit, FortiBleed demonstrates how determined threat actors can build long-term, industrial-scale credential harvesting operations that remain valuable long after individual security flaws have been patched.

The campaign came to light after security researcher Volodymyr Diachenko discovered an exposed database containing credentials linked to tens of thousands of FortiGate firewalls. its estimated the dataset contained credentials for more than 73,000 internet-facing devices across 194 countries, with many of the credentials independently verified as genuine. While the scale of the leak is alarming, the methods used to obtain these credentials are arguably even more significant.

##  Campaign Specifics

Unlike incidents driven by a single zero-day vulnerability, FortiBleed appears to be the result of several attack techniques working in tandem over an extended period. Reports suggest the attackers combined brute-force attacks, credential stuffing, previously stolen credentials and cracked SSL VPN authentication hashes to build a continually expanding database of valid administrator accounts. Researchers also observed billions of authentication attempts against FortiGate VPN appliances alongside attacks targeting Microsoft SQL Server instances, highlighting the level of automation and persistence behind the campaign.

What makes this particularly dangerous is that valid credentials can bypass many traditional security controls. Once an attacker has legitimate administrator credentials, they no longer need to exploit software vulnerabilities, they can simply log in. This makes malicious activity significantly more difficult to detect and allows attackers to move quickly from internet-facing devices into the wider network.

The campaign also reinforces an important lesson for defenders: applying security patches alone is not always enough. Fortinet has stated that FortiBleed is not linked to a newly disclosed vulnerability, but instead appears to stem from previously compromised credentials combined with sustained brute-force activity against exposed devices. That distinction is significant because it changes the defensive response. Keeping appliances fully up to date remains essential, but organisations should also assume that administrative credentials may already have been compromised and respond accordingly.

### Mitigation
For organisations that rely on FortiGate appliances, the priority should be to rotate all administrative credentials, enable multi-factor authentication wherever possible, review privileged accounts for unnecessary access, and audit firewall configurations for any signs of unauthorised changes. Security teams should also examine historical VPN and administrative login activity for suspicious behaviour and ensure that management interfaces are not unnecessarily exposed to the internet.

Ultimately, FortiBleed is another reminder that modern cyber attacks increasingly focus on compromising identities rather than exploiting software alone. Threat actors recognise that stolen passwords, authentication tokens and trusted accounts often provide a faster, quieter and more reliable route into an organisation than investing time in developing new exploits.