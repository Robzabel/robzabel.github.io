---
layout: post
title: Who are BlackNevas Ransomware Group?
---

![_config.yml]({{ site.baseurl }}/images/BNransomware.jpg)

## BlackNevas Background

BlackNevas, also known by the name of “Trial Recovery”, are a ransomware and data extortion group who’s operations date back to late 2024. The group have claimed 22 victims in total across the legal, technology, manufacturing and critical national infrastructure (CNI) sectors, in over five different countries. In each attack, victim data is stolen, before the groups ransomware (a derivative of Trigona) is deployed to encrypt files and systems. Previously, BlackNevas threatened victims that if they did not pay the ransom, their data will be auctioned off through an affiliate ransomware group’s dark web data leak site (DLS), in what is now a common practice of double extortion. Around May 2025, BlackNevas launched their own DLS where they publish a sample of the stolen data and information about the victim company as well as the negotiation status.

---

## DLS Overview

BlackNevas’ DLS appears to be still under construction. With the lack of contact details page, brand logo and relevant favicon, the onion site comes across as unfinished.

Insert image of contact page

The **Publications** page looks like it has had the most attention of the developers, displaying a tile for each victim specifying the company name and website along with the reported annual revenue and statistics of the data that was stolen. Each tile has an AI generated image that appears to be the BlackNevas group sat around a table on laptops, with the victim’s company name in the background. This image gives way to a carousel of sliding thumbnail pictures taken from the stolen data including publicly identifiable information (PII) of staff or customers, invoices, trade secrets or database dumps.

Insert Image of publications page

The **Statistics** and **Files** pages are of equal low-quality design and build. The statistics page simply lists metrics such as total victim count and total leaked data size. On the files page, there are no actual files available to be viewed or downloaded, apart from one document under the heading of “test55” which contains a file with the name “Новый текстовый документ.txt” which is Russian for “New Text Document.txt”.

---

## Diamond Model

Insert Diamond model



## Victim Selection

BlackNevas do not have a bias when it comes to target selection. From the victims that have been breached, it is deductible that large scale enterprises in the legal sector have been the majority of targets; however, target selection appears opportunistic rather than specific.

## Initial Access

As with most ransomware attacks, BlackNevas gain initial access into a target environment through three main methods:

* Logging in with legitimate employee credentials gained through phishing, found in data leaks or stolen through info stealer malware.
* Exploitation of public facing services that have un-patched known vulnerabilities (N-day).
* Spear phishing employees and social engineering them into running the ransomware file.



## Ransomware Binary

The BlackNevas ransomware is written for different operating systems including Windows, Linux and ESXi, it also employs several techniques for obfuscation, stealth, replication and persistence. Although sophisticated, the binary files do not utilise anti-sandbox or anti-debugging evasion techniques which has allowed it to be studied. SentinelOne have done an in-depth reversal of all binary types, in which they discovered the following key characteristics:

* **A double encryption mechanism:** Victim files are encrypted with multiple layers of the AES algorithm, and the keys are then further encrypted with and RSA algorithm.
* **File extensions:** Encrypted files are given the extension of “.-encrypted” or “.ENCRYPTED”
* **Persistence:** Registry run keys are modified to run the binary on start up.
* **Propagation:** The malware uses SMB from enumeration and spreading capabilities.
* **The ransom note:** A file called “how\_to\_decrypt.txt” containing the ransom note is written to every directory containing an encrypted file.



---

## Extortion

Insert image of ransom note

The only publicly available examples of the ransom note (at the time of writing) were written before BlackNevas had their own Onion site. The note informs victims that their files have been encrypted and that they have 7 days to pay a ransom before the decryption keys are deleted and their information is auctioned off. This is then followed by a warning about tampering with files in an attempt to decrypt them and some steps to download the Tor browser.

An interesting aspect of the note is that, to communicate with BlackNevas, the victim needs to email a @usa.com email address, created with the specified computer ID. Since this note is hard coded, an email addresses must be created per victim and updated in the note before the binary is compiled.

---

## Conclusion

Although being active for over a year, still not much is known about the group BlackNevas. They have stayed out of the mainstream and avoided the public eye while also tallying up a significant number of victims. It appears that the group may have started out as an affiliate of the more established ransomware gangs which would explain why the ransom note pointed victims to the Onion sites of KillSec, Hunters International, DragonForce, etc. But now it appears that they are running the whole process from initial access to negotiation themselves.

Indicators such as the unfinished website, low tech communication methods and using ransomware derived from code written by other authors shows that the group is still evolving and finding its place in the ransomware ecosystem. The Cyrillic named file, under the directory of test on their DLS, could point to the group being of Russian origin; however, there is no concrete evidence that is where they are based.
With a busy end to 2025, BlackNevas look set to carry on operations into the new year at pace and they will be a name to watch out for in future.



---

## Recommendations

Patch an update systems regularly including Network Attached Storage (NAS), virtualization platforms such as VMware ESXi and host/server Operating Systems (OS).

Implement strong access control for users through multifactor authentication, password policy coherence and apply the principles of least privilege.

Continuous monitoring through SIEM/EDR solutions and fine tuning of detection rules.

Rigorous backup solutions and a diligent disaster recovery plan should be in place before the worst case scenario happens.

Network segmentation through virtual local area networks (VLAN) will not stop an attacker from achieving their goals but it will go a long way to slowing them down.



---

## IOCs

### SHA256 Hashes of Known Samples

23642a78addcffd124db133a2dd2fcd2d1bdb060dd1e41da33cb18eec7a88867
2b9fe8a2629727470be1c928f7c9be7e2ea6cc22fb12f971902bf9cea8b16afb
360758c296310ba428d0d52c90e31c05fc43d5889282fa840283cf468f2378e8
3d09e930305cb3aa4ca54a39b0e3749f083d432f202606c8adac8455014b47fc
43f145fccec00f1e100ec3377eaf0ab60df3b9c5291b8011e05141cc04704be1
49fcbd606ff10d4661e222b8910ab7829d1668e3c97f1bab7eb51e8ec7d799a5
501821a19ccf59830789849beff94238736adb4b213870a511890c5c8efab2a6
623f3e98908962669e48edd414dbb67e9d4e204f677998fdcc9c2d790816a67f
713392f009bc133f24b3271379a4ac147e1a7782b6a1ac957c1fda69d676b550
840b1c580bfd15ca3eb1cc94cf479f63b93285d2599bc2e3cd361e3f5a340f19
8a2d6d27ffcc66400a640d3c9c9e6becb90c04c5bab452cac56f999c48a04d63
910cc03d64bf09f53cdf3b83068cc46368c23a061c2e1ed5df0e3a35d6c9e084
95e744ddcc2e8f89f6c6e25503eff2eb5e70e98f6989bb4a4e93f17b09448e78
9d9c146910f294b3e2a755f76e8066cd2edfac057ff54f00f405e2f9e8b9e51a
a0630e2a81775e8334ea9f8cac73cebf1b9a70507ea3347c0c2eba82c80219a6
a331504acf589be5d11202232a7a93eeb4fe6b053beea231d9a0a661bcaf3fd6
b0dfaf509de38749c49afcb3cd34d27126044bb77cc16896b02ebced6f95db02
b2353fce403b079735a606294c4ffc20a71f1c6b16ec15e94f554beafcddd1ea
bad3c2f72ef2be522a554a9615dc93027416a3d4048f77519fca5104fabba1f9
bf4adad2eb1163369c133ae61c181a3f91ef8640a457e9c4e72d77a60fbfa7ab
c08a752138a6f0b332dfec981f20ec414ad367b7384389e0c59466b8e10655ec
c0fc61631a20c373ce17e939e09cfb4f5179c9e0788e80079b4ee8986afe89bd
d953bce4d87f5837ce318481e3a1b6617cf64af976043d3b4b4866475bb31972
def75a41435dc28430097a7e116b2d17526ce2b0172995618f2749b0d732f7ea
e7706a633f24679c7550a31b96088dda8f772c98f64daee7cfbf0dc17a4a8338
eb8cbc4a0eae33bfdc4ecb99d033c81224b005e55588ceb86346f2b2d3fd790f

### Email Addresses

amsomar\[@]consultant\[.]com
black4over\[@]newlookst\[.]com
suppcarter\[@]uymail\[.]com
paymeuk\[@]consultant\[.]com
Serina5Murrock@email\[.]com
oxicavalon@myself\[.]com
avalonsupp\[@]consultant\[.]com
biosannetsuabvg\[@]mail\[.]com
compsupp\[@]techie\[.]com
corubete\[@]dr\[.]com
milford\[@]usa\[.]com
murrock\[@]consultant\[.]com
ovtaitonine\[@]usa\[.]com
toxicavalon\[@]toke\[.]com
varentsujikyuke\[@]mail\[.]com
widemoucerpco\[@]mail\[.]com



### TOR Address

hxxp\[:]//ctyfftrjgtwdjzlgqh4avbd35sqrs6tde4oyam2ufbjch6oqpqtkdtid\[.]onion



## Sources

* AHN Lab – https://asec.ahnlab.com/en/90080/
* SentinelOne – https://www.sentinelone.com/anthology/blacknevas/















Next you can update your site name, avatar and other options using the \_config.yml file in the root of your repository (shown below).



!\[\_config.yml]({{ site.baseurl }}/images/config.png)



The easiest way to make your first post is to edit this one. Go into /\_posts/ and update the Hello World markdown file. For more instructions head over to the \[Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub.

