# Level01

In this level i tried the same hack that i did in the first level, silly me, ofcourse it did not works
While searching in the internet on how to become a hacker, i came across this artice
[Linux Privilege Escalation – Writable passwd file](https://steflan-security.com/linux-privilege-escalation-writable-passwd-file/#:~:text=The%20%2Fetc%2Fpasswd%20file%20is,to%20escalate%20privileges%20to%20root.)

It says:
- The /etc/passwd file typically has file system permissions that allow it to be readable by all users of the system (world-readable),

- The /etc/passwd file is used in Linux operating systems to store user information such as user hashes, groups, home directory and more.

- If improper file permissions are used for this file, this could allow attackers to escalate privileges to root.

Passwd File & Format:

- The passwd file used to store user hashes although it no longer does, as these are now stored in the /etc/shadow file. The reason why this was changed is that some of the information stored in the passwd file has to be world-readable for the operating system to operate correctly, so hashes were moved to the shadow file which is normally only accessible by root.

then I tried to read that file
```bash
cat /etc/passwd
```
```bash
# output:
...
level08:x:2008:2008::/home/user/level08:/bin/bash
level09:x:2009:2009::/home/user/level09:/bin/bash
level10:x:2010:2010::/home/user/level10:/bin/bash
level11:x:2011:2011::/home/user/level11:/bin/bash
level12:x:2012:2012::/home/user/level12:/bin/bash
level13:x:2013:2013::/home/user/level13:/bin/bash
level14:x:2014:2014::/home/user/level14:/bin/bash
flag00:x:3000:3000::/home/flag/flag00:/bin/bash
flag01:42hDRfypTqqnw:3001:3001::/home/flag/flag01:/bin/bash
...
```
- x: Information used to validate a user's password. The format is the same as that of the analogous field in the shadow password file, with the additional convention that setting it to "x" means the actual password is found in the shadow file, a common occurrence on modern systems

but here the user flag01 contains this value: 42hDRfypTqqnw, which means this is the actual password or the hashed one, so let's try crack it with different tools, the first method was not working well so i tried john the cracker

```bash
echo "flag01:42hDRfypTqqnw:3001:3001::/home/flag/flag01:/bin/bash" > flag
john flag --show
# output:
# flag01:abcdefg:3001:3001::/home/flag/flag01:/bin/bash
# 1 password hash cracked, 0 left
# the password is abcdefg
su flag01
getflag
Check flag.Here is your token : f2av5il02puano7naaf6adaaf
```
