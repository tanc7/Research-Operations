# Overview: OP. DIAMOND SHARK. March 31st, 2017
This is the official research notes for OPERATION DIAMOND SHARK, the upcoming phase of LISTER UNLIMITED penetration testing research, by CHANG TAN LISTER.

# Hypothesis
Mobile devices are not known to have consistent IP addresses because of (a) proximity to cell tower (b) relative movement speed of victim

However, MMS messaging has static email addresses. For example if my phone number is 

310-123-4567 then it is represented in T-Mobile's MMS network as...
13101234567@tmomail.net

All you need to know is:

1. Their phone number
2. What cellular carrier they are on
3. Whether or not they have data plans enabled
4. Whether or not that they are connected to that data plan at the moment of transmission, OR if they are using Wi-Fi
5. The MMS/Email server that represents that carrier

# The Flaw of Planned Obsolesence and Trendy New Devices
Furthermore, Cellular Manufacturers have consistently left their customers behind in much needed patch updates for their customers and outdated Android devices. In short, OLDER Android and iPhones should be "easier to hack".

# Objectives

1. Attempt to compromise a Android system remotely
2. Use a reverse Meterpreter shell as a APK
3. Attempt to use a embedded picture, commonly sent by MMS
4. Use a chain-mail scheme in order to spread the malware, among other "21st Century Mobile Device Nuisances"
5. Try to incorporate social media crowdsourcing schemes in order to prove my point

# Parameters

1. We are going to use our own devices for this OP
2. The author, CTL, has several Android devices with varying versions, between Android 6.0, 7.0, KitKat, and Lollipop.
3. We are considering searching for Android Firmware Emulators in order to better simulate real life vulnerabilities

# 'Stagefright' Vulnerability
https://www.exploit-db.com/docs/39527.pdf

http://www.pcworld.com/article/2953052/security/most-android-phones-can-be-hacked-with-a-simple-mms-message-or-multimedia-file.html

Researcher: Joshua Drake

Firm: Zimperium

URL: https://www.zimperium.com/

The worst part is that the section I have commented on, "Flaw of Planned Obsolesence and Trendy New Devices", is actually confirmed. Some phones may NEVER see the day tha they are patched

This vulnerability allows remote code execution when...
1. You receive a MMS
2. Receive a modified video file
3. Or going to embedded media content on a webpage

August 2016 Article on "Stagefright": http://www.androidcentral.com/stagefright

ASLR may prevent the attacker from reliably injecting into a Android process (Address Space Layout Randomization)
That means anyone that has Android v.4.0 and up are technically immune. At least to certain aspects.
Furthermore, stock antivirus software such as Lookout, can make you able to detect exploits taking advantage of Stagefright.

Not true! ASLR bypassed here: https://www.exploit-db.com/exploits/40436/
Second one here: https://www.exploit-db.com/exploits/39640/

Compatible MP4 Payload Generator Here: https://www.exploit-db.com/exploits/38124/
Bug fixes for that exploit here: https://null-byte.wonderhowto.com/forum/use-stagefright-exploit-0164488/

Other links here:
https://www.exploit-db.com/exploits/38226/
https://www.exploit-db.com/exploits/40436/

# Metasploit Supports Stagefright Vulnerability
Only as a link formatted exploit. Not exactly sure how it works, it may be a malicious web URL type of injection. 

exploit/android/browser/stagefright_mp4_tx3g_64bit

Default options:

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   SRVHOST  0.0.0.0          yes       The local host to listen on. This must be an address on the local machine or 0.0.0.0
   SRVPORT  8080             yes       The local port to listen on.
   SSL      false            no        Negotiate SSL for incoming connections
   SSLCert                   no        Path to a custom SSL certificate (default is randomly generated)
   URIPATH                   no        The URI to use for this exploit (default is random)

Advanced options:

   Name                    Current Setting  Required  Description
   ----                    ---------------  --------  -----------
   ContextInformationFile                   no        The information file that contains context information
   DisablePayloadHandler   false            no        Disable the handler code for the selected payload
   EnableContextEncoding   false            no        Use transient context when encoding payloads
   ListenerComm                             no        The specific communication channel to use for this service
   SSLCipher                                no        String for SSL cipher spec - "DHE-RSA-AES256-SHA" or "ADH"
   SSLCompression          false            no        Enable SSL/TLS-level compression
   URIHOST                                  no        Host to use in URI (useful for tunnels)
   URIPORT                                  no        Port to use in URI (useful for tunnels)
   VERBOSE                 false            no        Enable detailed status messages
   WORKSPACE                                no        Specify the workspace for this module
   
Information from the official Rapid7 Metasploit Website, basically any device with SELinux either disabled or in permissive mode:

This module exploits a integer overflow vulnerability in the Stagefright Library (libstagefright.so). The vulnerability occurs when parsing specially crafted MP4 files. While a wide variety of remote attack vectors exist, this particular exploit is designed to work within an HTML5 compliant browser. Exploitation is done by supplying a specially crafted MP4 file with two tx3g atoms that, when their sizes are summed, cause an integer overflow when processing the second atom. As a result, a temporary buffer is allocated with insufficient size and a memcpy call leads to a heap overflow. This version of the exploit uses a two-stage information leak based on corrupting the MetaData that the browser reads from mediaserver. This method is based on a technique published in NorthBit's Metaphor paper. First, we use a variant of their technique to read the address of a heap buffer located adjacent to a SampleIterator object as the video HTML element's videoHeight. Next, we read the vtable pointer from an empty Vector within the SampleIterator object using the video element's duration. This gives us a code address that we can use to determine the base address of libstagefright and construct a ROP chain dynamically. NOTE: the mediaserver process on many Android devices (Nexus, for example) is constrained by SELinux and thus cannot use the execve system call. To avoid this problem, the original exploit uses a kernel exploit payload that disables SELinux and spawns a shell as root. Work is underway to make the framework more amenable to these types of situations. Until that work is complete, this exploit will only yield a shell on devices without SELinux or with SELinux in permissive mode.

# Examples of Stagefright-Compatible Exploit
https://github.com/jduck/cve-2015-1538-1

It is a payload generator for a specific Android Device Model

Another official example here: https://www.exploit-db.com/exploits/38226/

Appears to be a payload generator

# 'APK Payload-to-PNG File' Vulnerability
https://www.blackhat.com/docs/eu-14/materials/eu-14-Apvrille-Hide-Android-Applications-In-Images-wp.pdf

http://corkami.googlecode.com/svn/trunk/src/angecryption/angecrypt.py # Former location of APK-to-PNG format crypter
https://github.com/cryptax/angeapk # New Location of APK-to-PNG crypter, usage of this is described on Page #5 of the BlackHat PDF Link

I was Wrong... Apparenty the Cryptax Repo is about the drawing of the images, the actual credit belongs to Ange Albertini. Use the following links below for research notes
https://blog.fortinet.com/2014/03/31/angecryption-at-insomni-hack # That contains instructions on how to reencrypt what could POSSIBLY be a reverse meterpreter generated as a APK into a payload posing as a PNG image, a file format universally accepted by cellular providers as permissible to send via MMS

These links are merely POCs (Proof of Concepts). A entirely new application must be written for our intended usage. 


# Resources

http://basicstate.com/htm/page.htm # List of many of the possible domains that a phone number could resolve as
https://github.com/tanc7/Research-Operations/blob/master/OP-DIAMOND%20SHARK/CellularMMSEmailWordlist.txt # Same thing as a wordlist

