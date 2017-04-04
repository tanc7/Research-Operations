# Research Parameters
Yesterday, I, "Smoke Jaguar", successfully used the Stagefright exploit (one of many), to hack into my own phone. I have typed the conclucions in a different article in the same directory.

This time, I decided to refine the technique offered by Joshua Drake JDuck at his repo, in order to create a more capable session.

# Sources
http://www.security-faqs.com/what-is-rop-and-how-do-hackers-use-it.html
Joshua Drake's technique and exploit uses what is called ROP (Return Oriented Programming), as described by the upper link

While JDuck didn't explicitly mention this, ROP is a good way to bypass ASLR, which Google implemented to prevent StageFright exploits from working starting with Android 5.0+.

https://www.offensive-security.com/metasploit-unleashed/generating-payloads/

This here is a guide on generating metasploit shellcode, including how to include the elimination of bad bytes in Metasploit

"Page 76 of Grey Hat Python" by Justin Seitz

Explains how to debug shellcode that is crashing, including a neat little python program on how to locate badchars. 
This requires the installation and use of python 2.7 on Windows in order to use the immunity debugger immlib library. 

# JDuck's Source Code (Python)
https://github.com/jduck/cve-2015-1538-1

Starting on Line 125 of JDuck's exploit, is the function "def build_rop". The shellcode is a linux/armle/shell_reverse_tcp type on metasploit. And the actual shellcode starts at line 142 ending at line 180.

# New Idea

JDuck's shellcode was back in the year of 2015. By now, Metasploit already has some capable Android-specific Meterpreter shells that could do a much better job. 

This may take longer than usual, but it should be as easy as generating a msfvenom

payload/android/meterpreter/reverse_https (STAGED) or payload/android/meterpreter_reverse_https (INLINE)

payload, and tweaking JDuck's exploit to make it work. So this time, running the script will generate a infected mp4 file that has a instant Meterpreter upgrade.

# Notes and Disclaimers

1. Be forewarned that non-rooted devices were discovered to have limited capabilities, as described in OPERATION SMOKE JAGUAR. You cannot GEOLOCATE a victim or do a SMS dump without having the devices rooted first
2. Furthermore you cannot use the Stagefright listener anymore, remember now that the shellcode is a Meterpreter stager, and it must complete the second stage (the connect-back stage that will be sent by listener machine) or else it'll fail
3. Its probably not wise to create a INLINE payload, because one delivery vector to the desired MMS exploit is via Email-to-MMS. And we all know that emails have attachment size limits and spam filter limits.
4. I "Smoke Jaguar", am not much of a programmer or hacker. I only figured out how to use Python last month, and I been on GitHub for about half a month. Still learning this stuff right now. Will take me a while. 

# Proposed Solutions

# PS #1. 
We can overcome the filesize limits by replacing the initial MMS payload with a auto-executing script, that downloads the later stages, which is a idea I took from Skiddie's UAC Duck (see below)
# PS #2. 
One of the "stages" will be a entire rootkit meant to unlock Android phones. However, different cell manufacturers have different methods of unlocking, and their own anti-tamper mechanisms. There is no generic exploit as far as I can tell.
# PS #3. 
The second stage carries the Meterpreter Stager payload. It's fairly simple, it will connect back to the listener upgrading it to...
# PS #4. 
The third stage, the Meterpreter Inline. As long as the rootkit properly went off, then we have full access to the victim smartphone as well as geolocation + SMS dumping + voice recording + webcam spying.

