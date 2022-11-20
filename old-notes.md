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
