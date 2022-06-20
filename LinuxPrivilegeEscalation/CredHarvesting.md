# Credential Harvesting

During Linux Privilage Escalation, credentials can be hidden all over the system in configuration files, logs, or other low hanging fruits.

## Finding Config Files

```
for i in $(echo ".conf .config .cnf");do echo -e "\nFile extension: " $i; find / -name *$i 2>/dev/null | grep -v "lib\|fonts\|share\|core" ; done
```

## Find Creds in Config Files
```
for i in $(find / -name *.cnf 2>/dev/null | grep -v "doc\|lib");do echo -e "\nFile: " $i; grep "user\|password\|pass" $i 2>/dev/null | grep -v "\#";done
i
```

## Find OS Notes
```
find /home/* -type f -name "*.txt" -o ! -name "*.*"
```

## Find Scripts
```
for i in $(echo ".py .pyc .pl .go .jar .c .sh");do echo -e "\nFile extension: " $i; find / -name *$i 2>/dev/null | grep -v "doc\|lib\|headers\|share"; done
```

## Find Cronjobs
```
cat /etc/crontab
```
```
ls -la /etc/cron.*/

```

## Find SSH Keys
### Private Keys
```
grep -rnw "PRIVATE KEY" /home/* 2>/dev/null | grep ":1"
```
### Public Keys
```
grep -rnw "ssh-rsa" /home/* 2>/dev/null | grep ":1"
```

## Bash History
```
tail -n5 /home/*/.bash*
```
## Log Enumeration
```
for i in $(ls /var/log/* 2>/dev/null);do GREP=$(grep "accepted\|session opened\|session closed\|failure\|failed\|ssh\|password changed\|new user\|delete user\|sudo\|COMMAND\=\|logs" $i 2>/dev/null); if [[ $GREP ]];then echo -e "\n#### Log file: " $i; grep "accepted\|session opened\|session closed\|failure\|failed\|ssh\|password changed\|new user\|delete user\|sudo\|COMMAND\=\|logs" $i 2>/dev/null;fi;done
```
## Browser Creds

### Firefox Default Creds 
```
ls -l ~/.mozilla/firefox/ | grep default 
```
Use the directory results for the next command.
```
cat ~/.mozilla/firefox/<default directory>/logins.json | jq
```
'jq' is a commandline JSON processor

This will produce some encrypted credentials. You can use the open source tool Firefox Decrypt to decrypt those credentials: https://github.com/unode/firefox_decrypt
