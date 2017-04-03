# Research-Operations
These are heavily redacted documentation on my personally-run research projects about penetration testing. Full disclosure is not available online. 

The Author, is not willing to cooperate with LE, nor entities that are both Domestic and Foreign. He expects them to "figure it out themselves" from what the Author has disclosed in this document. 

# OPERATION KLONDIKE

Purpose: Test the overall effectiveness of various RATs (Meterpreter being a example) against various operating systems, most prominently Microsoft Windows and it's vectors of transmission

Conclusions:
1. Since Windows 8.x and 10, Cybersecurity measures have dramatically improved.
2. Multiple obstacles stand in the way of allowing attackers to install malware into targeted Windows Devices.
3. And yet these same safeguards do not extend to Windows 7, which only has UAC to protect it, and it's up to the responsibility of the user to prevent breaches.
4. Windows 8.x and 10 has the following safeguards, by default, without aftermarket software
  (a) User Account Control
  (b) SmartScreen that causes a blue dialog box to pop up confirming with the user to install unusual programs
  (c) Windows Defender can prevent the RAT from running
  (d) Mandatory Windows Updating, while reviled by the public, actually keeps the user well-protected
  (e) Sample Submission, Enabled By Default: Submits samples of previously unknown and suspected malware (a Meterpreter encoded payload further modified with Veil-Evasion PE Scrambler and Hyperion) to Microsoft for analysis
5. As well as aftermarket options such as BitDefender. BitDefender is far more aggressive in identifying suspected malware and can "freeze" the Meterpreter as it attempts to contact the listener.
6. Meanwhile, Windows Defender may still remain unaware of a payload generated by 4(e) for UP TO eight hours.
7. Second opinion scanners, such as HitManPro Heuristics Detection, is able to catch the malware, no matter what measures were used.
8. Windows Defender is now aware of, and can remove, persistence modules installed via Registry Hacks.
9. Keystroke Injection, also known commonly as "Bad USB Attack", "HID Keyboard Attack" and also demonstrated by the proprietary "USB Rubber Ducky" device, can evade UAC, but not when the injection binary completes the downloading of the secondary payload. At that point, it is up to the attacker to figure out how to evade active Windows Defender. 

# OPERATION SMOKE JAGUAR

Purpose: Test the vulnerabilities of smartphone operating systems and modern-day mobile device antiviruses.

Conclusions:
1. The effectiveness of Android security measures, at least for Android v 6.0, is far behind that of modern Microsoft Windows
2. Rooted Android devices are at bigger risk of disclosure of sensitive information. Greater capabilities are discovered within Meterpreter shells that infected ROOTED devices. Including SMS Dumping, SMS Impersonation, Call Log and Address Book Dumping, and both Cellular Network & WLAN Geolocation with the accuracy of about "a city block".
3. But ALL Android devices are VULNERABLE if the user, FAILS to adhere to common sense security measures. NON-ROOTED devices can still have their microphones tampered and recorded, photo-cameras being remote controlled and/or live-video recording feeds produced.
4. In theory, a attacker should be able to create a INLINE reverse shell, containing a RAT (Remote Access Trojan), along with a full ROOTKIT, so that way as soon as the victim restarts their phone, their device could be remotely "rooted", granting full access of private information to the attacker.
5. A proposed transmission vector is SMS/MMS to Email communication. See OP: Diamond Shark.
6. Secondary proposed transmission vector, as enabled by the Arms-Commander Project. Infecting a legitimate Android APK with malware and uploading it to a popular "App Store".

# OPERATION DIAMOND SHARK

Purpose: Expand further into the vulnerabilities found within cellular communications network. Operation DS is a offshoot of OP: SJ.

Conclusions:

1. Operation Diamond Shark is a partial success https://github.com/jduck/cve-2015-1538-1
2. The Command Shell is both active and persistent
3. Only requires a victim's phone number
4. On your end it requires the python script on jduck's repo
5. You need to rename Stagefright_CVE-2015-1538-1_Exploit.py as "mp4.py" and then run it
6. Parameters is callback IP and callback port and output file. 
7. Payload size approximately 1.9MB
8. The payload seems to be able to persist through restarts, remote termination (sessions -K)
9. Also deleting the text message doesn't do anything
10. LookOut AV fails to stop it
11. May require a full factory reset
12. However the shell is bugged. Probably because of using the default "SPRAY" parameter for memory injection, causing the shell to crash with no effect on victim phone, but a new command shell will spawn anyways.
13. Given that a exact MMS address can be derived from (1) Phone number and (2) Carrier name list: https://github.com/tanc7/Research-Operations/blob/master/OP-DIAMOND%20SHARK/CellularMMSEmailWordlist.txt it is not hard for anyone to use 

Test Parameters and Hypotheses:

1. Since about a decade ago, it is discovered that you can SMS/MMS text to a Email Address. Not for free though.
2. In the header of the received Email, your phone number is actually a Email Address, which contains (a) the phone number (b) the mail server of your cellular provider
3. In Theory, a person skilled in customizing a reverse shell, can create a payload that carries the following elements
  (a) Stage 1 payload Stager: A simple script of some sort that will download a much larger payload (likely a GitHub Repository)
  (b) Stage 2 Crafted Rootkit: Covertly "roots" a Android device in preparation for...
  (c) Stage 3 Fully Self-Contained Reverse Shell + RAT: Enables all of the capabilities as described in OP: Smoke Jaguar.
4. The original SmartPhone Pentest Framework provided by Georgia Weidmann's Bulb Security has now been deprecated, and now is Dagah Mobile Device Penetration Testing Framework. However, a few remnants of the research remains and is best to start here, which I forked from other Repos: https://github.com/tanc7/MobileApp-Pentest-Cheatsheet. She has also kindly provided to us a torrent file for her original kali 1.06 VM image that may contain the SPF Framework: http://www.mininova.org/tor/13311502/
  (a) In the cheatsheet, it covers both Android and Apple mobile devices
  (b) Confirms the vulnerabilities to test for in Android APK Malware Injection, which AC already incorporates
  (c) Confirms of the SMS/MMS transmission vector for malware. 
5. It is also known that mobile devices have "IP addresses", but it is a terrible idea to use that for pentesting purposes.
  (a) The IP address constantly changes due to the availability and proximity of local cell towers. It is the cell tower that leases the unique IP.
  (b) Within the vicinity of Las Vegas, my mobile tablet has been known to possess five different IP addresses at least. 
  (c) But we do know, that phone numbers + SMS/MMS + Email MAY represent a static address. Try it, go text yourself to your email address. Say "Hello" or something (but you might get charged for it). 
