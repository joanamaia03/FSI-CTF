# Trabalho realizado na Semana #14

# Setup 
Inicialmente descobrimos o endereço da nossa Virtual Machine assim como o nome da interface
- `interface=br-926a65a62492`
- `ip=10.9.0.1`

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook13/image.png)

## Lab Task Set 1: Using Scapy to Sniff and Spoof Packets

### Task 1.1: Sniffing Packets

#### Task 1.1A

```
#!/usr/bin/env python3
from scapy.all import *

def print_pkt(pkt):
    pkt.show()
    
pkt = sniff(iface=['br-926a65a62492', 'enp0s3'], filter='icmp', prn=print_pkt) 
```

Alteramos o nome da interface do script de python para o nome da nossa interface.

- Fizemos o ficheiro python executável
`chmod a+x task1.py`
- Corremos com privilégios root
`task1.py > out.txt `
- Mudamos para a conta seed e corremos sem privilégios root

```
su seed
task1.py > out1.txt
```

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook13/image3.png)

Reparamos que conseguimos correr o script com permissões root mas sem elas não nos é permitido executar o script e analisar pacotes.

#### Task 1.1B

- Capturar apenas o pacote ICMP

```
#!/usr/bin/env python3
from scapy.all import *

def print_pkt(pkt):
    pkt.show()
    
pkt = sniff(iface=['br-926a65a62492', 'enp0s3'], filter='icmp', prn=print_pkt) 
```

- Capturar qualquer pacote TCP que venha de um determinado IP e com número de porta de destino 23.

```
#!/usr/bin/env python3
from scapy.all import *

def print_pkt(pkt):
    pkt.show()
    
pkt = sniff(iface=['br-926a65a62492', 'enp0s3'], filter='tcp and src host 10.9.0.5 and dst port 23', prn=print_pkt)
```

Testamos com o comando `telnet 10.9.0.1 23` para ver se recebemos os pacotes tcp correspondentes ao sender 10.9.0.5 com porta destino de 23

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook13/image4.png)

- Os pacotes de captura vêm ou vão para uma sub-rede específica.

```
#!/usr/bin/env python3
from scapy.all import *

def print_pkt(pkt):
    pkt.show()
    
pkt = sniff(iface=['br-926a65a62492', 'enp0s3'], filter='net 128.230.0.0/16', prn=print_pkt)
```

### Task 1.2: Spoofing ICMP Packets

Para demonstrar o Spoofing de um pacote ICMP 

```
from scapy.all import *

# Definir o IP origem que é arbitrario e o IP de destino
src_ip = '10.9.0.37' 
dst_ip = '10.9.0.1'  # Change this to the target's IP address

# Criar pacote IP
ip_header = IP(src=src_ip, dst=dst_ip)

# Criar objeto ICMP
icmp_packet = ICMP()

# Dar stack ao IP e ao ICMP
spoofed_packet = ip_header / icmp_packet

# Mandar o pacote spoofed
send(spoofed_packet)

print(f"Sent spoofed ICMP packet from {src_ip} to {dst_ip}")

```
![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook13/image5.png)

Observamos pacotes ARP (Address Resolution Protocol) enquanto utilizamos o Wireshark, isso sugere que a rede está a tentar resolver o endereço de hardware.
O pacote de spoofing foi enviado com sucesso, se tivessemos utilizado um ip ja registado na ARP table veriamos um pacote ICMP ao inves de tipo ARP.

### Task 1.3: Traceroute

```
from scapy.all import *

def traceroute(destination, max_hops=30):
    for ttl in range(1, max_hops + 1):

        packet = IP(dst=destination, ttl=ttl) / ICMP()

        reply = sr1(packet, timeout=1, verbose=0)

        if reply is None:
            print(f"{ttl}. *")
        elif reply.haslayer(IP):
            src_ip = reply.getlayer(IP).src
            print(f"{ttl}. {src_ip}")

            if src_ip == destination:
                break

# Example usage
destination_ip = '10.9.0.6'
traceroute(destination_ip)
```

A função traceroute recebe um destino IP e um número máximo de saltos como opções. Usa um loop para enviar pacotes ICMP com incremento no valor TTL. Para cada TTL, espera por uma resposta usando sr1.

Ao testarmos com a maquina A vemos que so um salto existe porque estao na mesma subnetwork. Mas quando testamos com 8.8.8.8 vemos os saltos todos que acontecem.

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook13/image6.png)

### Task 1.4: Sniffing and-then Spoofing

```
from scapy.all import *

def spoof_icmp_reply(packet):
    if ICMP in packet and packet[ICMP].type == 8:  # ICMP echo request
        src_ip = packet[IP].src
        dst_ip = packet[IP].dst
        icmp_id = packet[ICMP].id
        icmp_seq = packet[ICMP].seq

        spoofed_packet = IP(src=dst_ip, dst=src_ip) / ICMP(type=0, id=icmp_id, seq=icmp_seq)

        send(spoofed_packet, verbose=0)

sniff(filter='icmp', prn=spoof_icmp_reply)
```

Este script é executado na VM e monitoriza a LAN através de sniffing de pacotes. Sempre que deteta um pedido de `echo` ICMP, envia imediatamente uma resposta de `echo` usando a técnica de spoofing de pacotes.

Quanto aos três comandos ping do contentor do utilizador:

ping 1.2.3.4: Como é um host inexistente na Internet, o container do utilizador não receberá uma resposta de `echo` legítima. No entanto, o seu programa envia uma resposta spoofed de eco, fazendo parecer que o host está vivo.

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook13/image7.png)

ping 10.9.0.99: Este é um host inexistente na LAN. Semelhante ao primeiro caso, o seu programa envia uma resposta spoofed de `echo`.

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook13/image8.png)

ping 8.8.8.8: Este é um host existente na Internet. O container do utilizador receberá uma resposta de `echo` legítima do host real, e o seu programa pode enviar também uma resposta spoofed, resultando em duas respostas.

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook13/image9.png)
