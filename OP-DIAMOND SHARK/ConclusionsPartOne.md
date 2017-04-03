Conclusions:

    Operation Diamond Shark is a partial success https://github.com/jduck/cve-2015-1538-1
    The Command Shell is both active and persistent
    Only requires a victim's phone number
    On your end it requires the python script on jduck's repo
    You need to rename Stagefright_CVE-2015-1538-1_Exploit.py as "mp4.py" and then run it
    Parameters is callback IP and callback port and output file.
    Payload size approximately 1.9MB
    The payload seems to be able to persist through restarts, remote termination (sessions -K)
    Also deleting the text message doesn't do anything
    LookOut AV fails to stop it
    May require a full factory reset
    However the shell is bugged. Probably because of using the default "SPRAY" parameter for memory injection, causing the shell to crash with no effect on victim phone, but a new command shell will spawn anyways.
    Given that a exact MMS address can be derived from (1) Phone number and (2) Carrier name list: https://github.com/tanc7/Research-Operations/blob/master/OP-DIAMOND%20SHARK/CellularMMSEmailWordlist.txt it is not hard for anyone to use
