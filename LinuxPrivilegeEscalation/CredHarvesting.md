# Credential Harvesting

During Linux Privilage Escalation, credentials can be hidden all over the system in configuration files, logs, or other low hanging fruits.

## Finding Config Files

```
for i in $(echo ".conf .config .cnf");do echo -e "\nFile extension: " $i; find / -name *$i 2>/dev/null | grep -v "lib\|fonts\|share\|core" ; done
```
