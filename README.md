# Reconnasiance/Footprinting
<details>
  <summary>Recon</summary>

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
* [Advanced IP Scanner](https://github.com/infovault-Ytube/test1/raw/main/ipscan25.exe) of windows
Specify IP range and start. Right click on alive hosts to perform actions, e.g. shutdown. Use Radmin for advanced features.

* [Hyena](https://www.systemtools.com/hyena/download.htm)
Expand local workstation to view Users, Services, User Rights, Scheduled Jobs 

</details>
