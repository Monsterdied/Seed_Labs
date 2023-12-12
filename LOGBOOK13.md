# LOGBOOK13 Sniffing and Spoofing
## Setup

Antes de começarmos o lab, precisamos de dar setup aos containers necessários para o guião:

```bash
dcbuild
dcup
```

Precisamos encontrar o nome da interface de rede correspondente na nossa máquina virtual, pois precisamos utilizá-la nos nossos programas:

```
[12/12/23]seed@VM:~/.../Labsetup$ ifconfig
br-1f43b629af2f: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.9.0.1  netmask 255.255.255.0  broadcast 10.9.0.255
        inet6 fe80::42:c4ff:fe69:d216  prefixlen 64  scopeid 0x20<link>
        ether 02:42:c4:69:d2:16  txqueuelen 0  (Ethernet)
        RX packets 148  bytes 7488 (7.4 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 312  bytes 57909 (57.9 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

## Task1.1A

Em cada terminal abrimos um shell para cada container:

```bash
[12/12/23]seed@VM:~/.../Labsetup$ dockps
323fb46ae1c0  hostB-10.9.0.6
93bfb074f21c  hostA-10.9.0.5
112fbb9ad809  seed-attacker

#Terminal host
docksh seed-attacker

#Terminal hostA
docksh 93b

#Terminal hostB
docksh 323
```

De seguida, criamos um ficheiro python no folder volumes, que contém o seguinte código:

```py
#!/usr/bin/env python3
from scapy.all import *
def print_pkt(pkt):
	pkt.show()
pkt = sniff(iface='br-1f43b629af2f', filter='icmp', prn=print_pkt)

```

Agora vamos dar permissões de executable ao programa e corre-lo com root privilege, usando a linha `chmod a+x sniffer.py`.

Antes de executar o sniffer.py, vamos executar o comando `ping 10.9.0.6` , na qual o hostA vai 'pingar' o hostB.

Vamos executar o sniffer.py no seed-attacker e vamos obter os seguintes resultados (ter em conta que isto é apenas uma porção pequena de resultados):

```
###[ Ethernet ]### 
  dst       = 02:42:0a:09:00:06
  src       = 02:42:0a:09:00:05
  type      = IPv4
###[ IP ]### 
     version   = 4
     ihl       = 5
     tos       = 0x0
     len       = 84
     id        = 35943
     flags     = DF
     frag      = 0
     ttl       = 64
     proto     = icmp
     chksum    = 0x9a25
     src       = 10.9.0.5
     dst       = 10.9.0.6
     \options   \
###[ ICMP ]### 
        type      = echo-request
        code      = 0
        chksum    = 0xde0b
        id        = 0x1e
        seq       = 0x1
###[ Raw ]### 
           load      = '\xef\x88xe\x00\x00\x00\x00\xeb\x13\x08\x00\x00\x00\x00\x00\x10\x11\x12\x13\x14\x15\x16\x17\x18\x19\x1a\x1b\x1c\x1d\x1e\x1f !"#$%&\'()*+,-./01234567'

```

Agora, vamos tentar executar sem privilégios root:
```bash
./sniffer.py
Traceback (most recent call last):
  File "./sniffer.py", line 5, in <module>
    pkt = sniff(iface='br-1f43b629af2f', filter='icmp', prn=print_pkt)
  File "/usr/local/lib/python3.8/dist-packages/scapy/sendrecv.py", line 1036, in sniff
    sniffer._run(*args, **kwargs)
  File "/usr/local/lib/python3.8/dist-packages/scapy/sendrecv.py", line 906, in _run
    sniff_sockets[L2socket(type=ETH_P_ALL, iface=iface,
  File "/usr/local/lib/python3.8/dist-packages/scapy/arch/linux.py", line 398, in __init__
    self.ins = socket.socket(socket.AF_PACKET, socket.SOCK_RAW, socket.htons(type))  # noqa: E501
  File "/usr/lib/python3.8/socket.py", line 231, in __init__
    _socket.socket.__init__(self, family, type, proto, fileno)
PermissionError: [Errno 1] Operation not permitted
```

Quando é executado sem privilégios de root, o programa não possui as permissões necessárias para aceder à interface de rede e, por conseguinte, não consegue capturar pacotes com sucesso.

## Task 1.1B

Para o primeiro, Capture only the ICMP packet, este já está feito, como demonstrado anteriormente:

Para o segundo, trocamos:

```py

pkt = sniff(iface='br-1f43b629af2f', filter='icmp', prn=print_pkt)

#por

pkt = sniff(iface='br-1f43b629af2f', filter='tcp && host 10.9.0.5 && port 23', prn=print_pkt)

```

