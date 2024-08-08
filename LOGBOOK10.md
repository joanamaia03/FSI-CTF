# Trabalho realizado na Semana #10

# Task 1: Frequency Analysis
Analisamos o ngram e fomos substituindo as letras mais comuns da língua inglesa até formarmos frases coerentes.

```
1-gram (top 20):
n: 488
y: 373
v: 348
x: 291
u: 280
q: 276
m: 264
h: 235
t: 183
i: 166
p: 156
a: 116
c: 104
z: 95
l: 90
g: 83
b: 83
r: 82
e: 76
d: 59
-------------------------------------
2-gram (top 20):
yt: 115
tn: 89
mu: 74
nh: 58
vh: 57
hn: 57
vu: 56
nq: 53
xu: 52
up: 46
xh: 45
yn: 44
np: 44
vy: 44
nu: 42
qy: 39
vq: 33
vi: 32
gn: 32
av: 31
-------------------------------------
3-gram (top 20):
ytn: 78
vup: 30
mur: 20
ynh: 18
xzy: 16
mxu: 14
gnq: 14
ytv: 13
nqy: 13
vii: 13
bxh: 13
lvq: 12
nuy: 12
vyn: 12
uvy: 11
lmu: 11
nvh: 11
cmu: 11
tmq: 10
vhp: 10
```
Acabamos com : tr 'nytmuxbqvprgahzldcfjiekso' 'ETHINOFSADGBCRUWYMVQLPXKJ' < ciphertext.txt > ciphertext1.txt, o que nos dá o texto decifrado.

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook10/image1.png)
![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook10/image2.png)

# Task 2: Encryption using Different Ciphers and Modes
```
AES-128-CBC:

$ openssl enc -aes-128-cbc -e -in plain.txt -out cipher_aes128cbc.bin \
-K 00112233445566778889aabbccddeeff -iv 0102030405060708

BF-CBC (Blowfish):

$ openssl enc -bf-cbc -e -in plain.txt -out cipher_bfcbc.bin \
-K 00112233445566778889aabbccddeeff -iv 0102030405060708

AES-128-CFB:

$ openssl enc -aes-128-cfb -e -in plain.txt -out cipher_aes128cfb.bin \
-K 00112233445566778889aabbccddeeff -iv 0102030405060708
```
Cada operação de encriptação cria um ficheiro de output, por exemplo cipher_aes128cbc.bin, cipher_bfcbc.bin, cipher_aes128cfb.bin. Estes ficheiros de output contêm data encriptada e vão ser diferentes para cada algoritmo de encriptação e modo.

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook10/image3.png)

```
openssl enc -aes-128-cbc -e -in plain.txt -out cipher_aes128cbc.bin -K 00112233445566778889aabbccddeeff -iv 0102030405060708
```

openssl: Ferramente da linha de comando para OpenSSL.

enc: Especifica o encode mode com cipher.

-aes-128-cbc: Método cipher.

-e: Usado para a encriptação.

-in plain.txt: Ficheiro input que estamos a encriptar.

-out cipher_aes128cbc.bin: Ficheiro output onde a data encriptada vai ser escrita.

-K 00112233445566778889aabbccddeeff: Key.

-iv 0102030405060708: Vetor de inicialização (IV) do cipher, representado por uma string hexadecimal.O IV é usado para garantir que textos idênticos são encriptados em diferentes ciphertexts.

Fizemos o mesmo com os outros métodos e encriptamos a imagem com ecb e cbc.

## Task 3:Encryption Mode – ECB vs. CBC

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook10/image4.png)
![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook10/image5.png)
![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook10/image6.png)
