# Research-Operations
These are heavily redacted documentation on my personally-run research projects about penetration testing. Full disclosure is not available online. 

The Author, is not willing to cooperate with LE, nor entities that are both Domestic and Foreign. He expects them to "figure it out themselves" from what the Author has disclosed in this document. 

# OPERATION KLONDIKE

Purpose: Test the overall effectiveness of various RATs (Meterpreter being a example) against various operating systems, most prominently Microsoft Windows and it's vectors of transmission

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

Test Parameters and Hypotheses:
1. Since about a decade ago, it is discovered that you can SMS/MMS text to a Email Address. Not for free though.
2. In the header of the received Email, your phone number is actually a Email Address, which contains (a) the phone number (b) the mail server of your cellular provider
3. In Theory, a person skilled in customizing a reverse shell, can create a payload that carries the following elements
  (a) Stage 1 payload Stager: A simple script of some sort that will download a much larger payload (likely a GitHub Repository)
  (b) Stage 2 Crafted Rootkit: Covertly "roots" a Android device in preparation for...
  (c) Stage 3 Fully Self-Contained Reverse Shell + RAT: Enables all of the capabilities as described in OP: Smoke Jaguar.
