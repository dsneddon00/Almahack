# Wordlists

Wordlists an like a hacker's screwdriver set: some are big, some are small, and some have different shapes. To use them effectively, you need to apply context and precision. This section should help you find the right tool for the job when bruteforcing or otherwise.

## SecLists

### Install on Kali
```
sudo apt install seclists
```
SecLists is a git repo containing all sorts of useful credential lists that you can use with most bruteforcing tools. Git Repo here: <https://github.com/danielmiessler/SecLists>

### Locating Seclists

```
seclists           

> seclists ~ Collection of multiple types of security lists

/usr/share/seclists
├── Discovery
├── Fuzzing
├── IOCs
├── Miscellaneous
├── Passwords
├── Pattern-Matching
├── Payloads
├── Usernames
└── Web-Shells
```

By simply typing in seclists, you can figure get a bigger picture of it's potential.

*Depending on your installation, SecLists may be in a different location. Be sure to account for that.*

### Default Credentials

```
/usr/share/seclists/Usernames/
/usr/share/seclists/Passwords/Default-Credentials
```
I personally recommend using *cirt-default-usernames.txt* and *ftp-betterdefaultpasslist.txt*.

### Leaked Databases

```
/usr/share/seclists/Passwords/Leaked-Databases 
```
Each iteration of *rockyou.txt* are my personal favorite. It contains credentials from a databreach containing over 32 million credentials ordered by popularity. You can find the full list online at <https://www.kaggle.com/datasets/wjburns/common-password-list-rockyoutxt>

## Custom Lists

### Cupp

You can use Cupp to generate custom password lists based on basic information such as a person's name, partner, children, pets, etc.

```
sudo apt install cupp
cupp -i
```

After running *cupp -i* simply input your desired keywords for the target and it will generate a list for you.

### Username Anarchy

Use Username Anarchy to generate potential usernames for a target.

```
git clone https://github.com/urbanadventurer/username-anarchy.git
./username-anarchy fname lname > target.txt
```
## Trimming Lists

In order to reduce time, trim your custom list so that it fits within the target's company password guidelines if they have any.

```
sed -ri '/^.{,7}$/d' wordList.txt		# Trim passwords with a length < 8
sed -ri '/[!-/:-@\[-`\{-~]+/!d' wordlist.txt	# Trim passwords without special chars
sed -ri '/[0-9]+/!d' wordlist.txt		# Trim passwords without numbers
```

