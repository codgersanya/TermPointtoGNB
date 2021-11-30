This script adds X2s between ENBs-GNBs via a user-friendly dialouge format.
The only input needed is the name of X2-relation(s).

Prerequisites:
The script may be started from offline amos/moshell on ENM
If it is run from moshell, ensure that ~/moshell/sitefiles/ipdatabase is up to date and includes the addresses of all the affected nodes.
Also, always ensure that variables are set correctly in your ~/.moshellrc so that login to nodes can work -based on nodenames only.

Usage:
After running the script (amos termpointtognb.mos) it asks whether you have a file with the list of X2s.
a) If the answer is yes, then the expected format is displayed.
Then it asks the path/and filename.
b) If the answer is no, then manual input dialogue opens.
The expected input format is: nodenames (ENB-GNB) uppercase letters + numbers, separated by hyphen (e.g: 69012BB2-69012BB3).
Having the list of wanted X2s, the script logins to each affected node automatically.
It checks the gnbid, the transport config (especially sctp for X2 and ipaddress).
It logins to the ENB checks, whether the wanted X2 already exists, verifies and corrects the IpAddresses -i needed and creates the termpoint if didn't exist.
Finally, Checks it's op-state.
It logins to the GNB and checks whether the X2 gets oper.
It fetches the reult in a table.
This loop isrepeated over all relations.
The script checks and displays if there's no contact to the nodes.
It checks whether ENB and GNB-functions exist on the nodes.

The script is written and tested on Ipsec X2s with endcX2IpAddrViaS1Active = false.

Results (example):
eNodeB_name X2_LDN_enB X2_operstate_enB gNB_name X2_LDN_gNB X2_operstate_gNB
69010BB2-69012BB2: ENodeBFunction=1,GUtraNetwork=1,ExternalGNodeBFunction=23430-69012,TermPointToGNB=23430-69012 0 (DISABLED) Warning: X2 CRE-FAIL on target GNB!
69010BB2 ENodeBFunction=1,GUtraNetwork=1,ExternalGNodeBFunction=23430-69010,TermPointToGNB=23430-69010 1 (ENABLED) 69010BB3 GNBCUCPFunction=gNBId69010,EUtraNetwork=1,ExternalENodeBFunction=auto234_30_2_69010,TermPointToENodeB=auto1 1 (ENABLED)
69010BB2-69013BB3: Warning: X2 CRE-FAIL on source GNB!

Structure:
The main script (termpointtognb_main.mos) has 3-additional subs, which need to be placed to the same folder.
termpointtognb_gnbsub
termpointtognb_enbsub
termpointtognb_xtworesultgnbsub
