# New Idea, Randomware Generator
So I had a discussion with someone in a meetup group that I won't disclose the identity of.

Basically he told me this.

"I don't want to lose anything in my hard drive. I need to back them up first. But, even though the data is valuable to me, I don't believe anyone else could make use of it."

And I asked him, "How much do you think it's worth?"

He replied, "To me, millions of dollars that covers all of my ideas".

I told him what if I encrypted everything on his hard drive and held it for ransom against him?, much to the laughter of my brother

"Well. Shit. Never thought of that."

# And That is how... OPERATION HELLS HORSES is born

I still need to do a lot of research. I can't guarantee a ETA of delivery of a PoC. But I want to see if through compromise by a reverse shell or exploit, whether or not I can remotely execute a payload that can encrypt a victim's hard drive on my own, and hold it for ransom, while maintaining control of the flow of public information to avoid LE from disrupting it.

Now where do I start?

# The Reverse Psychology Attack
According to this website, a well known security researcher and journalist by the name of Brian Krebs...
https://krebsonsecurity.com/2015/09/like-kaspersky-russian-antivirus-firm-dr-web-tested-rivals/#more-32052

At least half of the scanners on VirusTotal are "based on bullshit". In other words...

1. A completely harmless file
2. Encoded with a common malware toolkit like msfvenom
3. Submitted to VT
4. Will be flagged as malicious... REGARDLESS

That means... we can "break the trust" between client, and antivirus vendor!

The plan is this:

1. Download ALL of the important public files of a company (SEC filings, accounting period reports, financial statements)
2. Encode ALL of them with msfvenom/msfencode
3. Submit ALL of the HARMLESS files to VirusTotal to have VT flag them all as "viruses"
4. Wait for the clients (the targeted company that depended on that AV) to get frustrated and either ignore or uninstall the AV's active notifications

AND THEN...

5. Start the spearphishing campaign. Just go right ahead and rename one of the false-positive files as the malware/payload. The victim knows it'll get flagged, out of instinct they will open it anyways XD

