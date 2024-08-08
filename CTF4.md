# CTF4

## Contexto

- Um servidor Linux encontra-se à escuta na porta `4006` do host `ctf-fsi.fe.up.pt`. Para se ligar a este servidor pode utilizar-se o programa netcat da shell da seguinte forma: `nc ctf-fsi.fe.up.pt 4006`.

- Em particular, este servidor corre exatamente o mesmo sistema operativo (Ubuntu 20.04) que utilizamos nos SEED Labs. O seu comportamento há-de ser bastante similar ao estudado no SEED Lab sobre variáveis de ambiente. Relembra o que aprendeste...

- Em particular, encontrarás código de um script que corre regularmente no servidor. O administrator teve bastante cuidado em impedir que esse script releve informação inadvertidamente. A tua tarefa é subverter esse script para obter a flag escondida.


## Code Analysis

- Existe um arquivo 'shell script' denominado 'my_script.sh', que carrega variáveis de ambiente a partir do diretório `/home/flag_reader/env`. O proprietário deste arquivo possui permissões de root, fazendo com que, caso este script seja o mencionado no contexto, ele seja executado regularmente com permissões root no servidor, o que pode causar uma vulnerabilidade, tendo em conta que o mesmo chama programas executáveis, como o printenv.

- Existe também o arquivo env, mencionado no ponto anterior. Ao executar o comando `ls -l` que permite observar as permissões do arquivo, este pode ser modificado por um utilizador comum, como @nobody, que é o user atribuído quando entramos no servidor.

- Encontramos também um ficheiro com o nome 'main.c', que chama o comando `access("/flags/flag.txt", F_OK)`. Este pode indicar que a flag se encontra no ficheiro: '/flags/flag.txt'.

## Vulnerability

A vulnerabilidade surge da combinação de um script em execução com permissões de root, carregar variáveis de ambiente de um diretório que pode ser manipulado por usuários comuns e a presença de um arquivo indicando a localização de uma flag sensível.

## Exploit

~~~ 
mkdir -p /tmp/cansado

echo '#!/bin/bash

cat /flags/flag.txt > /tmp/cansado/canss.txt

chmod 777 /tmp/cansado/canss.txt' > /tmp/cansado/printenv.sh

chmod 777 /tmp/cansado/printenv

echo 'PATH=/tmp/cansado:/command:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin' > /home/flag_reader/env
~~~

O exploit que criamos funciona da seguinte forma:

1. O script printenv.sh é adicionado ao diretório /tmp/cansado e recebe permissões de execução.

2. A variável de ambiente PATH no arquivo /home/flag_reader/env é modificada para incluir /tmp/cansado como o primeiro diretório na sequência de pesquisa.

3. Quando o script "my_script.sh" é executado, tendo este privilégios de root, carrega as variáveis de ambiente que vão buscar executáveis primeiro no diretório /tmp/cansado.

4. Assim sendo, quando o "my_script.sh" tenta executar qualquer comando, a primeira procura será feita no diretório /tmp/cansado. O comando printenv é chamado, sendo executado o nosso script, uma vez que a primeira procura é feita nesse diretório, e não o original.

5. O nosso script "printenv.sh", por sua vez, lê a flag e escreve-a no arquivo "canss.txt".

Portanto, ao modificar a variável PATH e colocar um script malicioso no diretório que é pesquisado em primeiro lugar, exploramos o sistema para ler a flag sensível e armazená-la num arquivo ao qual possamos aceder.
