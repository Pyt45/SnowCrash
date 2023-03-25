# Level09
```bash
-rwsr-sr-x 1 flag09  level09 7640 Mar  5  2016 level09
----r--r-- 1 flag09  level09   26 Mar  5  2016 token # we can read the token but it contains some unprintable characters
cat token
f4kmm6p|=�p�n��DB�Du{��
```
Let's try excute the file
```bash
./level09 tnibj
token
./level09 token
tpmhr
# The program does encrypt the passed arg by increasing the character by its index, so let's reverse this program to obtain the old value
```

Create a program that decrypt the content of the token file

```bash
cat <<EOF > /var/tmp/decrypt.c
#include <stdio.h>

int main(int argc, char **argv) {
    for (int i = 0; i < strlen(argv[1]); i++) {
        char c = argv[1][i] - i;
        printf("%c", c);
    }
}
EOF
chmod 777 .
gcc -std=c99 /var/tmp/decrypt.c -o a.out
./a.out `cat token`
f3iji1ju5yuevaus41q1afiuq

su flag09

getflag -->
Check flag.Here is your token : s5cAJpM8ev6XHw998pRWG728z
```