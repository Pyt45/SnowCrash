# Level00

search for file that can run only as flag00
I run this command
```bash
ls -ls
# output: nothing i can use
# so i tried this one which was a hint from 42 vidoes
find / -group flag00 -exec ls -l {} \; 2>/dev/null
```
output of the above command gives me:
----r--r-- 1 flag00 flag00 15 Mar  5  2016 /usr/sbin/john
----r--r-- 1 flag00 flag00 15 Mar  5  2016 /rofs/usr/sbin/john

```bash
cat /usr/sbin/john
# output:
# cdiiddwpgswtgt
```

I run this command ```su flag00``` and asks me for a password, and i give it the output of ```cat /usr/sbin/john``` but it didn't works, so i tried to decode it using base64 but it gives me an error: invalid input
so i used the Cioher Identifier to analyze this txt and gives me a few methods to crack this txt, and i had tried Caesar Cipher method then it gives me a suspicious result, a weird looking password: `nottoohardhere`

```bash
su flag00
getflag
Check flag.Here is your token : x24ti5gi3x0ol2eh4esiuxias
su level01
```
