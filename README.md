# pfsense-syncookies-patch
pfSense Syncookies patch (for PF - Packet Filtering)

# how to
On this repo:
- Go to pfsense-syncookies.patch from this repository;
- Click in raw button;
- Copy the complete URI.

On pfSense:
- Install System_Patches pkg;
- Go to System -> Patches;
- Click in "Add New Patch";
- Put any description;
- Paste in URL/Commit ID;
- Change Path Strip Count to 1 and save;
- Fetch and apply;
- Go to Diagnostics -> Command Prompt and execute: /etc/rc.filter_configure;
- Enjoy.

# references:
- https://docs.opnsense.org/manual/firewall_settings.html#enable-syncookies
- https://man.freebsd.org/cgi/man.cgi?query=pf.conf&apropos=0&sektion=0&manpath=FreeBSD+14.2-RELEASE+and+Ports&arch=default&format=html
  
  		set syncookies never | always | adaptive
		     When syncookies are active, pf will answer	each incoming TCP  SYN
		     with  a syncookie SYNACK, without allocating any resources.  Upon
		     reception of the  client's	 ACK  in  response  to	the  syncookie
		     SYNACK,  pf  will	evaluate  the  ruleset and create state	if the
		     ruleset permits it, complete the three  way  handshake  with  the
		     target  host  and continue	the connection with synproxy in	place.
		     This allows pf to be resilient  against  large  synflood  attacks
		     which  would  run	the  state table against its limits otherwise.
		     Due to the	blind answers to every incoming	SYN  syncookies	 share
		     the  caveats  of synproxy,	namely seemingly accepting connections
		     that will be dropped later	on.

		     never     pf will never send syncookie SYNACKs (the default).
		     always    pf will always send syncookie SYNACKs.
		     adaptive  pf will enable syncookie	mode when a  given  percentage
			       of  the state table is used up by half-open TCP connec-
			       tions, as in, those that	saw the	initial	SYN but	didn't
			       finish the three	way handshake.	The thresholds for en-
			       tering and leaving syncookie mode can be	specified  us-
			       ing
	
				     set syncookies adaptive (start 25%, end 12%)
