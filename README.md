pf-IPrep
========

pf IP Reputation Manager

pfIP Reputation Manager will download Blocklists and can remove duplicate entries.
It can look for repeat Offenders in a /24 Range and condense the Block to a single /24 Line.
This is done using the "max", "dmax" and "pmax" variables.

Settings also allow for repeat Offending Ranges to be placed into a "Monitor/Match" List excluding the Blocked IPs.
Output files are single files 1)Downloaded version 2)Original Unmodified version 3) Final de-duplicate version

Three masterfiles are created 1) Mastercat (no Text) 2) Masterfile (Contains Blocklist Name with IP addresses)
3) Mastermatch file Used for Monitoring Ranges of Repeat Offenders.

Blocklists are compiled into Group/Tiers at the end of each scheduled Download process.
Individual Blocklists can also be used in the [ /pf ] and [ /ET ] folders.

Blocklists can be in .zip, .gz, .txt, Dotted Quad Notation, CIDR, or Range formats.
Blocklists can be Local Files or URLs, utilizing Fetch, Wget or Rsync.
Several Different "Processes" Are included to Capture the Correct Data.
pfIPrep will automatically download lists on a Fresh Install or when a new blocklist is added. No need to set bypass=yes

pfIPrep can output to 'Snorts IP Reputation Processor Blocklist' and 'OSSEC-HIDS IP Rep Blocklist'
It was designed primarily for pfSense and can reload the Blocklists automatically into pf.

The script downloads over 50 different Blocklists and performs a duplication check to reduce the size of the data. It can download .CSV, .TXT, ,GZ, .ZIP files and also scrape from certain websites that post only a web copy of their Blocklists. 

ie : ET, Spamhaus, IBlock,  dShield, Atlas, Alienvault etc.. I have been researching Blocklists for several Months and have found the current list to be beneficial in Blocking Malicious IPs.

It utilizes a tool called "Grepcidr" to make the de-duplication work.

It also looks at the number of IP addresses found in a /24 range and can condense the list and enter a /24 block instead. This is done in three ways

1) Using a "max" variable, if it finds over the Max variable it will perform a Maxmind Geoip Database lookup and will process a /24 block for configured Foreign Countries on anindividual Blocklist Basis.

2) Using a "dmax" variable  if it finds over the dmax variable it will perform a Maxmind Geoip Database lookup and will process a /24 block for configured Foreign Countries at the end of the download process on all of the Blocklists together.

3) Using a "pmax" variable, if it finds over the dmax variable it will process a /24 Block excluding Country Code whitelist at the end of the download process on all of the Blocklists together.

So I set max to 5, dmax to 5 and pmax to 50 in my setup.

Depending on how aggressive / conservative an admin wants to configure the processes or disable them completely and just use the de-duplication processes.

Script allows for Country Code Specific Blocklist utilizing the Maxmind GeoIP Database.

Recently added Support for Emerging Threats IQRisk IPRep Lists to the script. 


CHANGLOG - 2.3.3

  * Added Support to use the Emerging Threats IQRISK IP Reputation Lists   
      (Requires Subscription)
  * Some more of the Lists now support HTTPS downloads, and the collect lines
      have been updated.
  * Added a [ ./pfiprep killdb dskip  ] function which will reset the database with 
      the existing Downloaded Files
  * Moved Blocklist.de Blocklist from the Mail Server Section to the Regular  
      Section, as this list has more than Mail Server Blocklists. Refer to INFO URL in the 
      script.
  * Added a few other Blocklists
  * Script can now process IBlock Subscription Lists
  * Script can now process SquidBlock lists that are IP based.
  * Added "plog=yes" option to Log Errors to the pfSense System Log

I recommend running

[ ./pfiprep killdb   ]   with version changes  or  [  ./pfiprep killdb dskip  ]



