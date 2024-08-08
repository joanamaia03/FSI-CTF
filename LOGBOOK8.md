# Trabalho realizado na Semana #8

## Task 1 - Get Familiar with SQL Statements

Através do uso do comandos `use sqllab_users` e `show tables`, foi-nos possível selecionar a base de dados pretendida para que nos fosse exibida as tabelas da mesma. 

![iamge](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook8/image2.png)

Com o uso do comando `Select`, damos display à tabela credentials, sendo possível observar os dados da Alice.

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook8/image.png)

## Task 2 - SQL Injection Attack on SELECT Statement

### 2.1 - SQL Injection Attack from webpage

No código que nos foi fornecido, é possível observar que o código de aceitação do login se encontra no fim, verificando primeiro o input do nome e de seguida da password. Caso se comente o resto da query no fim do input do nome, a password não será verificada e ser-nos-á possível entrar no perfil do username que introduzimos.

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook8/image10.png)

### 2.2 - SQL Injection Attack from command line

Em vez de fazermos o exploit na webpage, usamos o comando curl para mandar uma request na qual inserimos o payload no nosso username.

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook8/image3.png)

### 2.3 - Append a new SQL Statement

Tendo em conta que o mysql tem medidas de segurança que não permitem fazer várias queries vindas do mesmo request, não nos foi possível inserir dados nas tabelas.


## Task 3 - SQL Injection Attack on UPDATE Statement

### 3.1 - Modify your own salary

Como temos como objetivo modificar o salário da Alice, fazemos uso do código ',salary='41414141 pois este modifica as informações da Alice. Ao abrirmos uma query dentro do forms que seleciona a tabela a editar, o valor que introduzirmos vai ser o novo valor correspondente à tabela da Alice.

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook8/image4.png)

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook8/image5.png)

### 3.2 - Modify other people' salary

Para esta parte, acrescentamos uma cláusula `WHERE`, selecionando qual o utilizador ao qual queremos modificar o salário.

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook8/image6.png)

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook8/image7.png)

### 3.3 - Modify other people' password


Fizemos uso de um site para dar hash a essa password, no nosso caso deadbeef e usamos o mesmo exploit das tasks anteriores para alterar a hash da password da base de dados.

![image](https://git.fe.up.pt/fsi/fsi2324/logs/l10g05/-/raw/main/Images/Logbook8/image9.png)

`', password = 'f49cf6381e322b147053b74e4500af8533ac1e4c' Where Name='Ted';`


