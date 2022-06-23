# Nmap

Nmap is a critical tool for penetration testing as it allows us to explore a system or a large network. It goes so far beyond simply identifying open ports, although it's create for that too. The Nmap man page is a fantastic read: <https://linux.die.net/man/1/nmap>

## Scanning a single ip

```
nmap <TARGET IP>
```

## Scanning Various Ports

```
nmap <TARGET IP> -p-		# all ports
nmap <TARGET IP> -p10-22	# scanning port range
nmap <TARGET IP> -p10,22	# specific port scan
nmap <TARGET IP> -F		# scanning top 100 ports
```

## Enumerating Services

```
nmap <TARGET IP> -sV		# scan service versions
nmap <TARGET IP> -O		# scan for operating system of target
nmap <TARGET IP> -A		# scan for operating system, service, and traceroute of target

```

## File Output

```
nmap <TARGET IP> -oA filename		# Stores results in normal, grepable, and xml formats. For individual formats, use -oN, -oG, and -oX respectively
```

## Performance

```
nmap <TARGET IP> -T<0-5>		# Timing. T0 being paranoid intrustion detection system evasion and T5 being insanely fast but also noisy.
nmap <TARGET IP> --stats-every=10s	# Displays stats of scan every 10 seconds.
nmap <TARGET IP> --min-rate 300		# Number of packets that will be sent simultaneously.

```
