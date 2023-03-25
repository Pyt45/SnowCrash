# Level14
## level topic: Basic Linux Anti Anti Debugging Techniques
There is no binary to debug or anything except getflag command<br>
Let's use gdb

```bash
gdb -q
file /bin/getflag
set height 0 # to see the full main assembly
set disassembly-flavor intel # Intel syntax
disas main
# Ouput
Dump of assembler code for function main:
   0x08048946 <+0>:     push   ebp
   0x08048947 <+1>:     mov    ebp,esp
   0x08048949 <+3>:     push   ebx
   0x0804894a <+4>:     and    esp,0xfffffff0
   0x0804894d <+7>:     sub    esp,0x120
   0x08048953 <+13>:    mov    eax,gs:0x14
   0x08048959 <+19>:    mov    DWORD PTR [esp+0x11c],eax
   0x08048960 <+26>:    xor    eax,eax
   0x08048962 <+28>:    mov    DWORD PTR [esp+0x10],0x0
   0x0804896a <+36>:    mov    DWORD PTR [esp+0xc],0x0
   0x08048972 <+44>:    mov    DWORD PTR [esp+0x8],0x1
   0x0804897a <+52>:    mov    DWORD PTR [esp+0x4],0x0
   0x08048982 <+60>:    mov    DWORD PTR [esp],0x0
   0x08048989 <+67>:    call   0x8048540 <ptrace@plt>
   0x0804898e <+72>:    test   eax,eax
   0x08048990 <+74>:    jns    0x80489a8 <main+98>
   ..................
   0x08048afd <+439>:   call   0x80484b0 <getuid@plt>
   0x08048b02 <+444>:   mov    DWORD PTR [esp+0x18],eax
   0x08048b06 <+448>:   mov    eax,DWORD PTR [esp+0x18]
   0x08048b0a <+452>:   cmp    eax,0xbbe
   0x08048b0f <+457>:   je     0x8048ccb <main+901>
   0x08048b15 <+463>:   cmp    eax,0xbbe
   0x08048b1a <+468>:   ja     0x8048b68 <main+546>
   0x08048b1c <+470>:   cmp    eax,0xbba
   0x08048b21 <+475>:   je     0x8048c3b <main+757>
   0x08048b27 <+481>:   cmp    eax,0xbba
   0x08048b2c <+486>:   ja     0x8048b4d <main+519>
   0x08048b2e <+488>:   cmp    eax,0xbb8
   0x08048b33 <+493>:   je     0x8048bf3 <main+685>
   0x08048b39 <+499>:   cmp    eax,0xbb8
   0x08048b3e <+504>:   ja     0x8048c17 <main+721>
   0x08048b44 <+510>:   test   eax,eax
   0x08048b46 <+512>:   je     0x8048bc6 <main+640>
   0x08048b48 <+514>:   jmp    0x8048e06 <main+1216>
   0x08048b4d <+519>:   cmp    eax,0xbbc
   0x08048b52 <+524>:   je     0x8048c83 <main+829>
   0x08048b58 <+530>:   cmp    eax,0xbbc
   0x08048b5d <+535>:   ja     0x8048ca7 <main+865>
   0x08048b63 <+541>:   jmp    0x8048c5f <main+793>
   0x08048b68 <+546>:   cmp    eax,0xbc2
   0x08048b6d <+551>:   je     0x8048d5b <main+1045>
   0x08048b73 <+557>:   cmp    eax,0xbc2
   0x08048b78 <+562>:   ja     0x8048b95 <main+591>
   0x08048b7a <+564>:   cmp    eax,0xbc0
   0x08048b7f <+569>:   je     0x8048d13 <main+973>
   0x08048b85 <+575>:   cmp    eax,0xbc0
   0x08048b8a <+580>:   ja     0x8048d37 <main+1009>
   0x08048b90 <+586>:   jmp    0x8048cef <main+937>
   0x08048b95 <+591>:   cmp    eax,0xbc4
   0x08048b9a <+596>:   je     0x8048da3 <main+1117>
   0x08048ba0 <+602>:   cmp    eax,0xbc4
   0x08048ba5 <+607>:   jb     0x8048d7f <main+1081>
   0x08048bab <+613>:   cmp    eax,0xbc5
   0x08048bb0 <+618>:   je     0x8048dc4 <main+1150>
   0x08048bb6 <+624>:   cmp    eax,0xbc6
   0x08048bbb <+629>:   je     0x8048de5 <main+1183>
   0x08048bc1 <+635>:   jmp    0x8048e06 <main+1216>
   0x08048bc6 <+640>:   mov    eax,ds:0x804b060
   0x08048bcb <+645>:   mov    edx,eax
   0x08048bcd <+647>:   mov    eax,0x8049090
   0x08048bd2 <+652>:   mov    DWORD PTR [esp+0xc],edx
   0x08048bd6 <+656>:   mov    DWORD PTR [esp+0x8],0x21
   0x08048bde <+664>:   mov    DWORD PTR [esp+0x4],0x1
   0x08048be6 <+672>:   mov    DWORD PTR [esp],eax
   0x08048be9 <+675>:   call   0x80484c0 <fwrite@plt>
   0x08048bee <+680>:   jmp    0x8048e2f <main+1257>
   0x08048bf3 <+685>:   mov    eax,ds:0x804b060
   0x08048bf8 <+690>:   mov    ebx,eax
   0x08048bfa <+692>:   mov    DWORD PTR [esp],0x80490b2
   0x08048c01 <+699>:   call   0x8048604 <ft_des>
   0x08048c06 <+704>:   mov    DWORD PTR [esp+0x4],ebx
   0x08048c0a <+708>:   mov    DWORD PTR [esp],eax
   0x08048c0d <+711>:   call   0x8048530 <fputs@plt>
   0x08048c12 <+716>:   jmp    0x8048e2f <main+1257>
   0x08048c17 <+721>:   mov    eax,ds:0x804b060
   0x08048c1c <+726>:   mov    ebx,eax
   0x08048c1e <+728>:   mov    DWORD PTR [esp],0x80490cc
   0x08048c25 <+735>:   call   0x8048604 <ft_des>
   0x08048c2a <+740>:   mov    DWORD PTR [esp+0x4],ebx
   0x08048c2e <+744>:   mov    DWORD PTR [esp],eax
   0x08048c31 <+747>:   call   0x8048530 <fputs@plt>
   0x08048c36 <+752>:   jmp    0x8048e2f <main+1257>
   0x08048c3b <+757>:   mov    eax,ds:0x804b060
   0x08048c40 <+762>:   mov    ebx,eax
   0x08048c42 <+764>:   mov    DWORD PTR [esp],0x80490e6
   0x08048c49 <+771>:   call   0x8048604 <ft_des>
   0x08048c4e <+776>:   mov    DWORD PTR [esp+0x4],ebx
   0x08048c52 <+780>:   mov    DWORD PTR [esp],eax
   0x08048c55 <+783>:   call   0x8048530 <fputs@plt>
   0x08048c5a <+788>:   jmp    0x8048e2f <main+1257>
   0x08048c5f <+793>:   mov    eax,ds:0x804b060
   0x08048c64 <+798>:   mov    ebx,eax
   0x08048c66 <+800>:   mov    DWORD PTR [esp],0x8049100
   0x08048c6d <+807>:   call   0x8048604 <ft_des>
   0x08048c72 <+812>:   mov    DWORD PTR [esp+0x4],ebx
   0x08048c76 <+816>:   mov    DWORD PTR [esp],eax
   0x08048c79 <+819>:   call   0x8048530 <fputs@plt>
   0x08048c7e <+824>:   jmp    0x8048e2f <main+1257>
   0x08048c83 <+829>:   mov    eax,ds:0x804b060
   0x08048c88 <+834>:   mov    ebx,eax
   0x08048c8a <+836>:   mov    DWORD PTR [esp],0x804911a
   0x08048c91 <+843>:   call   0x8048604 <ft_des>
   0x08048c96 <+848>:   mov    DWORD PTR [esp+0x4],ebx
   0x08048c9a <+852>:   mov    DWORD PTR [esp],eax
   0x08048c9d <+855>:   call   0x8048530 <fputs@plt>
   0x08048ca2 <+860>:   jmp    0x8048e2f <main+1257>
   0x08048ca7 <+865>:   mov    eax,ds:0x804b060
   0x08048cac <+870>:   mov    ebx,eax
   0x08048cae <+872>:   mov    DWORD PTR [esp],0x8049134
   0x08048cb5 <+879>:   call   0x8048604 <ft_des>
   0x08048cba <+884>:   mov    DWORD PTR [esp+0x4],ebx
   0x08048cbe <+888>:   mov    DWORD PTR [esp],eax
   0x08048cc1 <+891>:   call   0x8048530 <fputs@plt>
   0x08048cc6 <+896>:   jmp    0x8048e2f <main+1257>
   0x08048ccb <+901>:   mov    eax,ds:0x804b060
   0x08048cd0 <+906>:   mov    ebx,eax
   0x08048cd2 <+908>:   mov    DWORD PTR [esp],0x804914e
   0x08048cd9 <+915>:   call   0x8048604 <ft_des>
   0x08048cde <+920>:   mov    DWORD PTR [esp+0x4],ebx
   0x08048ce2 <+924>:   mov    DWORD PTR [esp],eax
   0x08048ce5 <+927>:   call   0x8048530 <fputs@plt>
   0x08048cea <+932>:   jmp    0x8048e2f <main+1257>
   0x08048cef <+937>:   mov    eax,ds:0x804b060
   0x08048cf4 <+942>:   mov    ebx,eax
   0x08048cf6 <+944>:   mov    DWORD PTR [esp],0x8049168
   0x08048cfd <+951>:   call   0x8048604 <ft_des>
   0x08048d02 <+956>:   mov    DWORD PTR [esp+0x4],ebx
   0x08048d06 <+960>:   mov    DWORD PTR [esp],eax
   0x08048d09 <+963>:   call   0x8048530 <fputs@plt>
   0x08048d0e <+968>:   jmp    0x8048e2f <main+1257>
   0x08048d13 <+973>:   mov    eax,ds:0x804b060
   0x08048d18 <+978>:   mov    ebx,eax
   0x08048d1a <+980>:   mov    DWORD PTR [esp],0x8049182
   0x08048d21 <+987>:   call   0x8048604 <ft_des>
   0x08048d26 <+992>:   mov    DWORD PTR [esp+0x4],ebx
   0x08048d2a <+996>:   mov    DWORD PTR [esp],eax
   0x08048d2d <+999>:   call   0x8048530 <fputs@plt>
   0x08048d32 <+1004>:  jmp    0x8048e2f <main+1257>
   0x08048d37 <+1009>:  mov    eax,ds:0x804b060
   0x08048d3c <+1014>:  mov    ebx,eax
   0x08048d3e <+1016>:  mov    DWORD PTR [esp],0x804919c
   0x08048d45 <+1023>:  call   0x8048604 <ft_des>
   0x08048d4a <+1028>:  mov    DWORD PTR [esp+0x4],ebx
   0x08048d4e <+1032>:  mov    DWORD PTR [esp],eax
   0x08048d51 <+1035>:  call   0x8048530 <fputs@plt>
   0x08048d56 <+1040>:  jmp    0x8048e2f <main+1257>
   0x08048d5b <+1045>:  mov    eax,ds:0x804b060
   0x08048d60 <+1050>:  mov    ebx,eax
   0x08048d62 <+1052>:  mov    DWORD PTR [esp],0x80491b6
   0x08048d69 <+1059>:  call   0x8048604 <ft_des>
   0x08048d6e <+1064>:  mov    DWORD PTR [esp+0x4],ebx
   0x08048d72 <+1068>:  mov    DWORD PTR [esp],eax
   0x08048d75 <+1071>:  call   0x8048530 <fputs@plt>
   0x08048d7a <+1076>:  jmp    0x8048e2f <main+1257>
   0x08048d7f <+1081>:  mov    eax,ds:0x804b060
   0x08048d84 <+1086>:  mov    ebx,eax
   0x08048d86 <+1088>:  mov    DWORD PTR [esp],0x80491d0
   0x08048d8d <+1095>:  call   0x8048604 <ft_des>
   0x08048d92 <+1100>:  mov    DWORD PTR [esp+0x4],ebx
   0x08048d96 <+1104>:  mov    DWORD PTR [esp],eax
   0x08048d99 <+1107>:  call   0x8048530 <fputs@plt>
   0x08048d9e <+1112>:  jmp    0x8048e2f <main+1257>
   0x08048da3 <+1117>:  mov    eax,ds:0x804b060
   0x08048da8 <+1122>:  mov    ebx,eax
   0x08048daa <+1124>:  mov    DWORD PTR [esp],0x80491ea
   0x08048db1 <+1131>:  call   0x8048604 <ft_des>
   0x08048db6 <+1136>:  mov    DWORD PTR [esp+0x4],ebx
   0x08048dba <+1140>:  mov    DWORD PTR [esp],eax
   0x08048dbd <+1143>:  call   0x8048530 <fputs@plt>
   0x08048dc2 <+1148>:  jmp    0x8048e2f <main+1257>
   0x08048dc4 <+1150>:  mov    eax,ds:0x804b060
   0x08048dc9 <+1155>:  mov    ebx,eax
   0x08048dcb <+1157>:  mov    DWORD PTR [esp],0x8049204
   0x08048dd2 <+1164>:  call   0x8048604 <ft_des>
   0x08048dd7 <+1169>:  mov    DWORD PTR [esp+0x4],ebx
   0x08048ddb <+1173>:  mov    DWORD PTR [esp],eax
   0x08048dde <+1176>:  call   0x8048530 <fputs@plt>
   0x08048de3 <+1181>:  jmp    0x8048e2f <main+1257>
   0x08048de5 <+1183>:  mov    eax,ds:0x804b060
   0x08048dea <+1188>:  mov    ebx,eax
   0x08048dec <+1190>:  mov    DWORD PTR [esp],0x8049220
   0x08048df3 <+1197>:  call   0x8048604 <ft_des>
   0x08048df8 <+1202>:  mov    DWORD PTR [esp+0x4],ebx
   0x08048dfc <+1206>:  mov    DWORD PTR [esp],eax
   0x08048dff <+1209>:  call   0x8048530 <fputs@plt>
   0x08048e04 <+1214>:  jmp    0x8048e2f <main+1257>
   0x08048e06 <+1216>:  mov    eax,ds:0x804b060
   0x08048e0b <+1221>:  mov    edx,eax
   0x08048e0d <+1223>:  mov    eax,0x8049248
   0x08048e12 <+1228>:  mov    DWORD PTR [esp+0xc],edx
   0x08048e16 <+1232>:  mov    DWORD PTR [esp+0x8],0x38
   0x08048e1e <+1240>:  mov    DWORD PTR [esp+0x4],0x1
   0x08048e26 <+1248>:  mov    DWORD PTR [esp],eax
   0x08048e29 <+1251>:  call   0x80484c0 <fwrite@plt>
   0x08048e2e <+1256>:  nop
   0x08048e2f <+1257>:  mov    eax,ds:0x804b060
   0x08048e34 <+1262>:  mov    DWORD PTR [esp+0x4],eax
   0x08048e38 <+1266>:  mov    DWORD PTR [esp],0xa
   0x08048e3f <+1273>:  call   0x8048520 <fputc@plt>
   0x08048e44 <+1278>:  jmp    0x8048ead <main+1383>
   0x08048e46 <+1280>:  mov    DWORD PTR [esp+0x4],0x8049281
   0x08048e4e <+1288>:  lea    eax,[esp+0x1c]
   0x08048e52 <+1292>:  mov    DWORD PTR [esp],eax
   0x08048e55 <+1295>:  call   0x80487be <afterSubstr>
   0x08048e5a <+1300>:  test   eax,eax
   0x08048e5c <+1302>:  jne    0x8048e89 <main+1347>
   0x08048e5e <+1304>:  mov    eax,ds:0x804b040
   0x08048e63 <+1309>:  mov    edx,eax
   0x08048e65 <+1311>:  mov    eax,0x8049294
   0x08048e6a <+1316>:  mov    DWORD PTR [esp+0xc],edx
   0x08048e6e <+1320>:  mov    DWORD PTR [esp+0x8],0x30
   0x08048e76 <+1328>:  mov    DWORD PTR [esp+0x4],0x1
   0x08048e7e <+1336>:  mov    DWORD PTR [esp],eax
   0x08048e81 <+1339>:  call   0x80484c0 <fwrite@plt>
   0x08048e86 <+1344>:  jmp    0x8048ead <main+1383>
   0x08048e88 <+1346>:  nop
   0x08048e89 <+1347>:  mov    eax,DWORD PTR [esp+0x14]
   0x08048e8d <+1351>:  mov    DWORD PTR [esp+0x8],eax
   0x08048e91 <+1355>:  mov    DWORD PTR [esp+0x4],0x100
   0x08048e99 <+1363>:  lea    eax,[esp+0x1c]
   0x08048e9d <+1367>:  mov    DWORD PTR [esp],eax
   0x08048ea0 <+1370>:  call   0x804874c <syscall_gets>
   0x08048ea5 <+1375>:  test   eax,eax
   0x08048ea7 <+1377>:  jne    0x8048a89 <main+323>
   0x08048ead <+1383>:  mov    eax,0x0
   0x08048eb2 <+1388>:  mov    edx,DWORD PTR [esp+0x11c]
   0x08048eb9 <+1395>:  xor    edx,DWORD PTR gs:0x14
   0x08048ec0 <+1402>:  je     0x8048ec7 <main+1409>
   0x08048ec2 <+1404>:  call   0x80484a0 <__stack_chk_fail@plt>
   0x08048ec7 <+1409>:  mov    ebx,DWORD PTR [ebp-0x4]
   0x08048eca <+1412>:  leave  
   0x08048ecb <+1413>:  ret    
End of assembler dump.

>> b *0x08048989 # set a break point
>> p $eax # print the value of eax return value of getuid
>> eax = -1
>> set $eax = 0
>> cont
>> b *0x08048afd # set another break point
>> cont
>> p $eax
>> eax = 2014, which the id of level14
>> set $eax=3014, id of flag14, cmd=id flag14 | awk -F'=' '{print $2}' | egrep -o "[0-9]+\($*" | tr -d '('
>> cont
>> Check flag.Here is your token : 7QiHafiNa3HVozsaXkawuYrTstxbpABHD8CPnHJ
```

[Basic Linux Anti Anti Debugging Techniques](https://www.stonedcoder.org/~kd/lib/14-61-1-PB.pdf)