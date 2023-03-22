./level09 tnibj
token
./level09 token
tpmhr

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