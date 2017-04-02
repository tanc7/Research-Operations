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

# OPERATION DIAMOND SHARK

Purpose: Expand further into the vulnerabilities found within cellular communications network. Operation DS is a offshoot of OP: SJ.
