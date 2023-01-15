+++
title = "Resources"
author = ["Delia Stephens"]
date = 2023-01-15
draft = false
description = "WIP resources compiled as I learn about cybersecurity."
+++

This is a <span class="underline">work-in-progress</span> compilation of useful commands, resources, etc. I've curated during my time doing various easy CTFs and online research. It is far from being either <span class="underline">complete</span> or <span class="underline">correct</span>, and serves mostly as a quick place to jot down things I've used during online exercises.


## Using this document {#using-this-document}

This document is written using [org-mode](https://orgmode.org/worg/orgcard.html) and exported to Hugo with [ox-hugo](https://ox-hugo.scripter.co/).

To insert code, type: `C-c C-, s`

To export, type: `C-c C-e H H`


## Useful External References {#useful-external-references}


### RFCs {#rfcs}

<https://www.rfc-editor.org/>


### Kali Linux Tools {#kali-linux-tools}

<https://www.kali.org/tools/>


### Steflan Security {#steflan-security}

<https://steflan-security.com/>


### CTF 101 {#ctf-101}

<https://ctf101.org/>


### Awesome Security {#awesome-security}

<https://github.com/sbilly/awesome-security>


## Linux Commands {#linux-commands}


### netstat {#netstat}

Shows the network status and protocol options.

To retrieve only active Internet connections, try:
`netstat -tulpn`


### ss {#ss}

Similar to `netstat`


### iptables {#iptables}

Used to set up, maintain, and inspet the tables of IPv4 and IPv6 packet filter rules in the Linux kernel.

Has the following commands: `accept`, `drop`, `return` (stop traversing the chain and resume at the next rule in the previous chain).

Can be used in concert with `ufw`


#### ufw {#ufw}

A more useful tool for packet filtering in Linux.


### ip address {#ip-address}

Shows you the IP address and other information. Part of the larger command `ip`.

To show the IP address info about one interface:

```bash
ip address | grep wlan0
```


### grep {#grep}

Print lines that match patterns.


### resolvectl status {#resolvectl-status}

Information about the DNS protocol on device interfaces.


### tcpdump {#tcpdump}

A packet capturing tool built into Linux which allows you to grab packets meeting particular conditions, write them to a file, etc. It's fairly complicated, so there's a guide [here](https://danielmiessler.com/study/tcpdump/) if you want it.

Also, here's a quick [cheat sheet](https://packetlife.net/media/library/12/tcpdump.pdf).

```bash
tcpdump -i INTERFACE -c COUNT -w FILE.pcap
```

```bash
tcpdump -ttnnvvS
```


## Linux File Locations {#linux-file-locations}


### DNS information {#dns-information}

`/etc/resolve.conf`


### Logs {#logs}

[Reference](https://www.cyberciti.biz/faq/linux-log-files-location-and-how-do-i-view-logs-files/)

`/var/log`

| Log filename                 | Contents                               |
|------------------------------|----------------------------------------|
| `auth.log`, `var/log/secure` | Authorization information              |
| `messages`                   | General messages                       |
| `kern.log`                   | Kernel logs                            |
| `cron.log`                   | cron jobs                              |
| `maillog`                    | Mail server log                        |
| `httpd`                      | Apache access and error logs directory |
| `lighttpd`                   |                                        |
| `nginx`                      | Nginx access and error logs            |
| `apt/`                       | apt-get command history                |
| `boot.log`                   | System boot log                        |
| `mysqld.log`                 | MySQL database server log file         |
| `utmp`, `wtmp`               | Login records                          |
| `yum.log`, `dnf.log`         | yum/dnf command log file               |


## Installing Tools {#installing-tools}

On this system, I have installed [katoolin](https://github.com/LionSec/katoolin), which allows a user to install the Kali linux tools using their repositories.

To run katoolin, navigate to `/usr/bin` and run the command: `sudo python2.7 katoolin`. Then, add Kali repositories and update; finally, you can actually install the tools.


## Reconnaissance {#reconnaissance}


### Wireshark {#wireshark}

Wireshark is a packet analysis tool which can be used to capture packets, filter them, and analyze them. (side note: there is another option called tcpdump. It seems useful, and there's a list of what you can do with it [here](https://jvns.ca/tcpdump-zine.pdf)).


#### Filtering with Wireshark {#filtering-with-wireshark}

More information can be found at [the Wireshark filtering page](https://www.wireshark.org/docs/wsug_html_chunked/ChWorkBuildDisplayFilterSection.html), but here are the basics.

| Operator     | Symbol     |
|--------------|------------|
| and          | &amp;&amp; |
| or           | ǁ​          |
| equals       | eq, ==     |
| not equal    | neq, !=    |
| greater than | gt, &gt;   |
| less than    | lt, &lt;   |

| Filter         | Syntax                  |
|----------------|-------------------------|
| IP Address     | ip.addr                 |
| IP Source      | ip.src                  |
| IP Destination | ip.dst                  |
| TCP Protocol   | tcp.port, protocol name |
| UDP Protocol   | udp.port, protocol name |


#### Address Resolution Protocol {#address-resolution-protocol}

An overview of ARP can be found at: <https://www.rfc-editor.org/rfc/rfc826>


#### ICMP {#icmp}

An overview of ICMP can be found at: <https://www.rfc-editor.org/rfc/rfc792>

ICMP type of 8 means that the packet is a request packet; type of 0 is a reply packet. If these codes are altered or don't seem correct, that's a great sign there's suspicious activity on the network.


#### TCP {#tcp}

An overview of TCP can be found at: <https://www.rfc-editor.org/rfc/rfc793>

TCP can be quite challenging to analyze. There are other tools, like RSA NetWitness and NetworkMiner, which make it slightly easier to analyze.

A TCP connection starts with the TCP handshake, which includes a [SYN], [SYN, ACK], and [ACK] packets. WHen the handshake is out of order, it includes packets like a [RST] packet, which could indicate that something is wrong.

If a port is not open, the acknoqledgement number will be 0.


### Nmap {#nmap}

Nmap is a network scanning tool which can be used to identify open ports, services operating on those ports, and live hosts on a given network.

Its documentation is available [here](https://nmap.org/docs.html).


#### Stealthily mapping out a network {#stealthily-mapping-out-a-network}

Useful reference available [here](https://unix.stackexchange.com/questions/188367/get-names-of-devices-on-the-network).


#### Determining which ports are open {#determining-which-ports-are-open}

When conductin a port scan, Nmap considers the following six states:

1.  Open: a service is listening on the specified port.
2.  Closed: no service is listening on the specified port, but the port is accessible.
3.  Filtered: Nmap isn't sure if the port is open or closed because the port isn't accessible (packets can't get to the port, or they can't get back; usually firewall filtering)
4.  Unfiltered: Nmap isn't sure if the port is open or closed, but the port is accessible (common with ARP scans)
5.  Open | Filtered: Nmap can't figure out if the port is open or filtered.
6.  Closed | Filtered: Nmap can't figure out if the port is closed or filtered.

<!--listend-->

```bash
sudo nmap -v TARGET_IP -Pn
```

<!--list-separator-->

-  TCP Connect Scan

    ```bash
    nmap -sT MACHINE_IP -v #verbose
    ```

<!--list-separator-->

-  TCP SYN Scan

    ```bash
    sudo nmap -sS MACHINE_IP -v
    ```

<!--list-separator-->

-  UDP Scan

    ```bash
    sudo nmap -sU MACHINE_IP -v
    ```


#### Determining services  with XML output {#determining-services-with-xml-output}

```bash
sudo nmap -v -sV -pDESIRED_PORTS -oX OUTPUT_NAME.xml TARGET_IP
```


### ARP Scan {#arp-scan}

arp-scan is a Kali Linux tool which can

Its documentation is available [here](https://www.kali.org/tools/arp-scan/#:~:text=arp%2Dscan%20is%20a%20command,sudo%20apt%20install%20arp%2Dscan).


#### Network Mapping {#network-mapping}

You can map a single host, a subnet, or a range of hosts, as specified in the documentation.

```bash
arp-scan XX.XX.XX.XX/SN
```

You can <span class="underline">randomize</span> the network scan with the flag -R or --random.


#### System Fingerprinting {#system-fingerprinting}


### Gobuster {#gobuster}

Gobuster is a tool written in Go that performs brute-force search on URI (directory and file), DNS subdomains, virtual host names, open Amazon S3 buckets. It uses a wordlist (on this computer `/usr/share/wordlists/`) to try and match to the desired target.

Its documentation is available [here](https://github.com/OJ/gobuster).


#### Directory busting on a website {#directory-busting-on-a-website}

```bash
gobuster dir -u TARGET_IP -w /usr/share/wordlists/dirb/common.txt
```

\*\*


## Exploitation {#exploitation}


### Remote shell with netcat {#remote-shell-with-netcat}


#### Creating a listener {#creating-a-listener}

```bash
nc -vnlp 9991 # 9991 is the port in the PHP reverse shell code
```


#### Stabilizing the shell {#stabilizing-the-shell}

If the host has Python install, it can be possible to "stabilize the shell" with a couple of shell commands:

```bash
python -c 'import pty; pty.spawn("/bin/bash")'
```

```bash
python -c 'import os; os.system("/bin/bash")'
```


### John the Ripper {#john-the-ripper}

John the Ripper is a password-cracking tool.


#### Going from an RSA private key to John the Ripper {#going-from-an-rsa-private-key-to-john-the-ripper}

```bash
/usr/share/ssh2john.py rsa_private_key > john_formatted_hash
```


#### Cracking a hash with John the Ripper {#cracking-a-hash-with-john-the-ripper}

```bash
john hash_to_crack wordlist
```

Example wordlist:  `/usr/share/wordlists/rockyou.txt`


### THC Hydra {#thc-hydra}

Hydra is another password-cracking tool. It's useful for cracking passwords on a remote system.


#### Cracking Example {#cracking-example}

```bash
hydra -l username -P wordlist.txt server service
```

`server` is the hostname or IP address of the target server
`service` is the service running on that server which you want to attack.

A detailed walk-through is available here: <https://tryhackme.com/room/hydra>


## Privilege Escalation {#privilege-escalation}


### [GTFOBins](https://gtfobins.github.io/) {#gtfobins}

A curated list of Unix binaries that can be used to bypass local security restrictions on misconfigured systems.

Typically, the steps to privilege escalation are:

1.  Determine which programs can be run as root.
2.  Search GTFOBins for the vulnerability corresponding to those files.


### Determining which programs can be run as root on current user {#determining-which-programs-can-be-run-as-root-on-current-user}

```bash
sudo -l
```


### Searching for files with SUID permission {#searching-for-files-with-suid-permission}


#### SUID {#suid}

Allows file users to run the file with effective permissions of the file owner.

```bash
find . -type f -user root -perm -4000 2>/dev/null
```


#### SGID {#sgid}

Allows file users to run file with group permission of file's owner.

```bash
find . -type f -user root -perm -2000 2>/dev/null
```


## Exploit Databases {#exploit-databases}


### Searchsploit {#searchsploit}

[searchsploit](https://www.exploit-db.com/searchsploit) is a command-line tool for exploit-DB which allows you to search exploits. It also saves copies locally on a user's machine.


#### Running from nmap output {#running-from-nmap-output}

```bash
searchsploit --nmap OUTPUT_NAME
```


#### Getting more specific about info about an exploit {#getting-more-specific-about-info-about-an-exploit}


## Metasploit {#metasploit}


## Reverse Engineering {#reverse-engineering}


### Useful Links {#useful-links}

[CTF 101](https://ctf101.org/reverse-engineering/overview/) provides a helpful overview, as well as more specific guides about how to reverse engineer.
[Godbolt](https://godbolt.org/) explains how different compilers will compile the same code.
