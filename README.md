# SnowCrash
## level00
 -> flag: x24ti5gi3x0ol2eh4esiuxias | find / -user flag00 -exec ls -l {} \; 2>/dev/null
## level01
 -> flag: abcdefg | cat /etc/passwd | grep "flag01" => flag01:42hDRfypTqqnw:3001:3001::/home/flag/flag01:/bin/bash
 -> then use scp to copy /etc/shadow to vm contain kali linux image
 -> then use john the ripper tool to crack the password
 -> echo "flag01:42hDRfypTqqnw:3001:3001::/home/flag/flag01:/bin/bash" > test ; john test -wordlist="wordlist" ; john --show test
 -> verfiy with john --show <(echo 42hDRfypTqqnw)
