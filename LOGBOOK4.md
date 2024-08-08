# Trabalho realizado nas Semanas #4 e #5

## Task 1: Manipulating Environment Variables

- Utilizamos os comandos `printenv` e `env` para listar as variáveis de ambiente do sistema 'SEEDS'. Notamos que ambos têm o mesmo resultado se executados no mesmo sistema sem argumentos adicionais. Após pesquisa, chegamos à conclusão que o comando `env` difere do `printenv`, pois permite-nos definir variáveis de ambiente com a sintaxe `env VAR=value`, onde a variável de ambiente 'VAR' recebe o valor 'value'.

![image](./Images/Captura_de_ecr%C3%A3_2023-10-17_222536.png)

- Foi utilizado o comando `export` para definir uma nova variável de ambiente e atribuir-lhe um valor. Para testar, decidimos criar uma variável 'HELLO' e defini-la como 'Hello World!' com o comando `export HELLO="Hello World!"`. Para verificar o valor da variável, utilizamos `echo $HELLO`, onde o `$` substitui a variável de ambiente pelo seu valor.

- Utilizamos o comando `unset` para remover a variável de ambiente previamente definida com o comando `unset HELLO`. Ao executar `echo $HELLO`, confirmamos que a variável de ambiente já não está definida.

![image](./Images/Captura_de_ecr%C3%A3_2023-10-17_223018.png)

## Task 2: Passing Environment Variables from Parent Process to Child Process

- Depois de compilar e executar o código reparamos que o 'child process' dá print às suas variáveis de ambiente. Ao utilizarmos o `> out1`, os prints do programa são registados no documento 'out1' para o podermos analizar posteriormente.

- Depois de comentarmos o `printenv` do 'child process' e descomentar  o `printenv` do parent process, recompilamos e executamos o programa com `> out2`. O parent process dá print às suas variaveis de ambiente.

![image](./Images/Captura_de_ecr%C3%A3_2023-10-17_223941.png)

- Ao comparar os ficheiros usando 'diff' `diff out1 out2`, reparamos que não existe output, o que significa que as variáveis de ambiente do parent são herdadas pelo processo child.

![image](./Images/Captura_de_ecr%C3%A3_2023-10-17_224105.png)

## Task 3: Environment Variables and execve()

- Começamos por compilar o programa myenv.c, correndo-o de seguida, executando o o /usr/bin/env através de um novo processo com o comando execve. Não há output.

- O terceiro argumento corresponde à forma como as variáveis de ambiente são manipuladas. Quando este é NULL, o ambiente do processo é completamente redefinido, fazendo com que o novo programa tenha um ambiente vazio e assim não haja retorno algum. Quando esse argumento é substituído por environ, o ambiente atual do processo que contém as variáveis de ambiente definidas no sistema é passado para o novo programa. Assim sendo, as variáveis de ambiente exibidas são as mesmas que as do processo e não as do programa. Esta mudança mantém o ambiente do processo original quando executado o programa.

![image](./Images/Captura_de_ecr%C3%A3_2023-10-17_224559.png)
![image](./Images/Captura_de_ecr%C3%A3_2023-10-17_224539.png)
![image](./Images/Captura_de_ecr%C3%A3_2023-10-17_224746.png)
![image](./Images/Captura_de_ecr%C3%A3_2023-10-17_224830.png)

## Task 4: Environment Variables and system()

- O comando "usr/bin/env" exibe as variáveis de ambiente do sistema, enquanto a função system() cria um novo processo que executa o comando especificado e redireciona a saída padrão desse processo para o terminal. Assim sendo, ao usar o comando mencionado fazendo uso da função system(), as variáveis de ambiente do sistema foram impressas no terminal.

- É uma forma de observar como é que as variáveis de ambiente são afetadas e que valores contêm quando um novo programa é executado usando a função system().

![image](./Images/Captura_de_ecr%C3%A3_2023-10-17_225246.png)

## Task 5: Environment Variable and Set-UID Programs

- Depois de compilarmos o programa que dá print às variáveis de ambiente e mudarmos a ownership do ficheiro para o root com o comando chown, usamos também o comando `chmod 4755`. Neste comando, o primeiro dígito 4 dá 'set' ao byte 'Set_UID' e os próximos 3 bytes em ordem alteram as permissões do owner, do grupo e do 'outros'.

![image](./Images/Captura_de_ecr%C3%A3_2023-10-17_225427.png)

- Os programas 'Set_UID' assumem os privilégios do dono do ficheiro durante a sua execução, rejeitando as do user que a executa.

- Mudamos 3 variáveis de ambiente, o PATH, o LD_LIBRARY_PATH e uma variável inventada ANY_NAME. Ao executar o programa reparamos que mesmo que as variáveis de ambiente tenham mudado, existe uma que não está presente, o LD_LIBRARY_PATH. Isto pode ser explicado pelos recursos de segurança dos programas 'Set_UID' que limitam as variáveis de ambiente que podem ser transmitidas para o programa. Tal acontece, visto que permitir que variáveis de ambiente arbitrárias sejam transmitidas para um programa Set-UID poderia abrir portas para várias formas de abuso ou exploração.

![image](./Images/Captura_de_ecr%C3%A3_2023-10-17_230022.png)
![image](./Images/Captura_de_ecr%C3%A3_2023-10-17_230056.png)
## Task 6: The PATH Environment Variable and Set-UID Programs

- Começamos por adicionar um path, usando a função export PATH=/home/diogo/Documents/FSI/Guiao\ 1/Labsetup/seed:$PATH, colocando-a em primeiro lugar na lista de paths.

- De seguida, compilamos o programa main que chama o ls e mudamos a sua ownership para root, usando o sudo chown root ls. Transformamos o programa em Set-UI, fazendo uso do comando sudo chmod 4755 ls.

![image](./Images/Captura_de_ecr%C3%A3_2023-10-17_230308.png)

- Quando testamos o programa main, vemos que funciona como expectado, com o normal funcionamento do ls.

- Criamos uma versão maliciosa do ls, que dá print à palavra "hacked" e inserimos no caminho que adicionamos à variável PATH. Corremos o código novamente, de modo a ver que essa mensagem é impressa para verificarmos que a nossa versão é a que é executada e não a original.

![image](./Images/Captura_de_ecr%C3%A3_2023-10-17_230552.png)
![image](./Images/Captura_de_ecr%C3%A3_2023-10-17_231121.png)

- Para testar se o nosso programa tem permissões root, mudamos o código do nosso programa malicioso para system("cat /var/log/firewalld"), uma vez que assim o programa só irá correr caso tenha permissões root. Verificamos que não temos permissões root, como explicado na nota do guião, uma vez que o programa shell tem uma medida que previne a execução do comando system em ficheiros Set-UID.
