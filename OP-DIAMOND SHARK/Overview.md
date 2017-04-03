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

# Resources
http://www.pcworld.com/article/2953052/security/most-android-phones-can-be-hacked-with-a-simple-mms-message-or-multimedia-file.html
Researcher: Joshua Drake
Firm: Zimperium
URL: https://www.zimperium.com/
