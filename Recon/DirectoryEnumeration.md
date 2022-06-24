# Directory Enumeration

Many SysAdmins, Web Developers, and the like often believe in "security by obscurity", meaning that something won't be found if it's simply "hidden". Fortunately for us, that can exploit that to broaden our attack vector.

## Gobuster

### Install

```
sudo apt install gobuster
```

*Note, you may need to install Golang to get it to work*

### Usage

```
gobuster dir -e -u http://<TARGET IP>/ -w /usr/share/wordlists/dirb/common.txt		# basic directory enum
```

## Ffuf

### Install

```
sudo apt install ffuf
```

### Usage

```
ffuf -u http://<TARGET IP>/FUZZ -w /usr/share/wordlists/dirb/common.txt			# basic directory enum
```
