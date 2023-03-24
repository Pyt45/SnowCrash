# Level02

Run this command:
```bash
ls -la
# output: intersting output, there is a file end with .pcap, it is a pcap file
```

What is a PCAP file? PCAP files are data files created using a program. These files contain packet data of a network and are used to analyze the network characteristics. They also contribute to controlling the network traffic and determining network status.

```bash
# from the host machine
scp -P 4242 level02@192.168.64.7:/home/user/level02/level02.pcap ~/Desktop/
password: f2av5il02puano7naaf6adaaf
```

You can analyze this pcap file using tcpdump or wireshark<br/>
Wireshark is easier to use, therfore we are going to use it<br/>
Open wireshark and choose to open the pcap file, in the navbar select analyze and the follow tcp stream<br/>
You will see the payload, select show data as hex dump<br/>
it will look like this<br/>
```
    000000D6  00 0d 0a 50 61 73 73 77  6f 72 64 3a 20            ...Passw ord: 
000000B9  66                                                 f
000000BA  74                                                 t
000000BB  5f                                                 _
000000BC  77                                                 w
000000BD  61                                                 a
000000BE  6e                                                 n
000000BF  64                                                 d
000000C0  72                                                 r
000000C1  7f                                                 .
000000C2  7f                                                 .
000000C3  7f                                                 .
000000C4  4e                                                 N
000000C5  44                                                 D
000000C6  52                                                 R
000000C7  65                                                 e
000000C8  6c                                                 l
000000C9  7f                                                 .
000000CA  4c                                                 L
000000CB  30                                                 0
000000CC  4c                                                 L
000000CD  0d                                                 .
```
Copy the hex after password `66745f77616e64727f7f7f4e4452656c7f4c304c04` and then convert it, hex to string<br/>
it will gives you: `ft_wandrNDRelL0L`
```bash
su flag02
getflag
Check flag.Here is your token : kooda2puivaav1idi4f57q8iq
```