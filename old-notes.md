# Old Notes


## ENUMERATION - SYSTEM, USERS, FILES, PROCESSES, SERVICES, TASKS, NETWORK INFO, RUNAS

### Get System Info
| Linux | Windows |
|:-----:|:-----:|
|```uname -a && cat /proc/version```|```systeminfo```|
### Get Current User
| Linux | Windows |
|:-----:|:-----:|
|```whoami```|```echo %USERNAME```|
### Who's Logged On Currently
| Linux | Windows |
|:-----:|:-----:|
|```who -a```|```?```|
### Get All Users On Machine
| Linux | Windows |
|:-----:|:-----:|
|```cat /etc/passwd```|```net user```|
### Get All Groups On Machine
| Linux | Windows |
|:-----:|:-----:|
|```cat /etc/group```|```net localgroup```|
### Get Password Hashes
| Linux | Windows |
|:-----:|:-----:|
|```cat /etc/shadow```|fgdump.exe / meterpreter hashdump / kiwi|
