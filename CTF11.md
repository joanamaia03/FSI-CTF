# CTF11

## Vulnerability Analysis
Esta vulnearbilidade consiste na escolha de números primos de modo a gerar o módulo RSA(n). Foi, então, necessário encontrar os primos p e q, próximos de 2^512 e 2^513.
Isto torna a fatorização do módulo n mais simples do que se os primos fossem escolhidos de maneira aleatória.

A chave pública RSA consiste em dois componentes principais: o módulo `n` e o expoente público `e`. 
A chave privada também é composta por dois componentes: o módulo `n` e o expoente privado `d`.
Se um atacante conseguir fatorizar o módulo n nos seus fatores primos p e q, então este pode calcular a chave privada.

Como podemos inferir os valores usados no RSA que cifraram a flag?
- Usando os primos fornecidos, p e q, para calcular o módulo `n=p*q` e de seguida gerar as chaves públicas e privadas.

Como podemos descobrir se a inferência está correta?
- Testando a nossa implementação do RSA, cifrando e decifrando mensagens. Caso seja possível recuperar a mensagem principal, a inferência está correta.

Como extrair a chave do criptograma recebido?
- Sabendo os primos, p e q, podemos calcular as chaves públicas e privadas e usando a chave privada conseguimos decifrar a flag cicfrada.

## Exploit
Inicialmente definimos uma série de variáveis: a flag codificada, a chave pública `e`, e o módulo `n`. De seguida, definimos p e q como primos grandes. 

No RSA, p e q são os primos secretos usados para gerar a chave privada. Neste caso, o script tenta  adivinhar os valores de p e q usando um loop e incrementando p e q até encontrar valores que são primos e que dividem `n` sem resto, quebrando assim a chave privada.
Uma vez que p e q são encontrados, o script calcula phi_n e assim consegue calcular a chave privada `d` como o inverso multiplicativo de `e mod(phi_n)`.

Por fim, o script decriptografa a flag codificada usando a chave privada `d` e o módulo `n`, e imprime a flag decodificada.

```
    def solve():

    # encoded_flag = "xxxxxxxxx"

    e = 0x10001
    # n = xxxx
    
    p = 2**512 + 1
    q = 2**513 + 1

    while True:
        if is_prime(p) and n % p == 0:
            break
        p += 1
    
    while True:
        if is_prime(q) and n % q == 0:
            break
        q += 1

    phi_n = (p - 1) * (q - 1)
    d = inverse(e, phi_n)

    flag = dec(unhexlify(encoded_flag), d, n)
    print(n == p * q)
    print(flag.decode())
```

