# ENUMERATION - SYSTEM, USERS, FILES, PROCESSES, SERVICES, TASKS, NETWORK INFO, RUNAS

## System & User Information

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

### Does Current User Have Special Priv

| Linux | Windows |
|:-----:|:-----:|
|```sudo -l```|```whoami /priv```|

### Get Current User's Command History

| Linux | Windows |
|:-----:|:-----:|
|```cat ~/.bash_history```|```doskey /history```(resets w/ new cmd.exe)|

## Network Information

### List Network Adapter Settings

| Linux | Windows |
|:-----:|:-----:|
|```ip addr show```|```ipconfig /all```|

### Show IP Routes

| Linux | Windows |
|:-----:|:-----:|
|```netstat -r```|```netstat -r```|

### Show All Listening Ports & Connections

| Linux | Windows |
|:-----:|:-----:|
|```netstat -anop```|```netstat -anop```|

## Interesting Files / Places to Look

### 
