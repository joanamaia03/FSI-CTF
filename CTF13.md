# CTF13

## Vulnerability Analysis

O Protocolo de Segurança de Camada de Transporte (TLS) é uma tecnologia projetada para garantir a segurança na transmissão de dados entre duas aplicações. O seu principal objetivo é proteger as informações durante a comunicação, assegurando que os dados não sejam interceptados por qualquer entidade externa indesejada.

O TLS atinge esse objetivo por meio de técnicas avançadas de criptografia, que transformam os dados numa forma ilegível para qualquer observador não autorizado. Dessa maneira, mesmo que terceiros tentem interceptar a comunicação, eles não conseguirão decifrar ou compreender os dados transmitidos. Essa camada de segurança é crucial para proteger informações sensíveis, como senhas, detalhes de pagamento e outros dados confidenciais, garantindo a integridade e a confidencialidade das comunicações online.

Neste CTF vamos focar maioritariamente no handshake protocol.

## Exploit

Para filtrar as comunicações desejadas no Wireshark, começamos por identificar o número aleatório, através do enunciado. 

Ao encontrar o "Client Hello", obtemos o frame start, e com o conhecimento do protocolo de Handshake, determinamos o frame end. Ao analisar o "Client Hello", identificamos a "cipher suite". 

Para encontrar todos os dados de aplicação criptografados, examinamos as partes de "Application Data" no Wireshark e navegamos até à camada de segurança de transporte para identificar os comprimentos. 

Finalmente, para encontrar a flag, localizamos o ponto onde identificamos o frame end e descemos até encontrar o tamanho da mensagem de Handshake criptografada. Ao juntar todas essas informações na ordem especificada no enunciado, obtemos a flag.

```
frame start: 814
frame end: 819
selected cipher suite: TLC_RSA_WITH_AES_128_CBC_SHA256
totaly encrypted data app exchanged: 1264
size of encrypted message: 80
```
flag{814-819-TLS_RSA_WITH_AES_128_CBC_SHA256-1264-80}
