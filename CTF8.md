#CTF8

## Vulnerability Analysis
Nos ficheiros identificamos que a base de dados usada é SQLite3 e encontramos uma vulnerabilidade de SQL Injection.

```
$username = $_POST['username'];
$password = $_POST['password'];             
$query = "SELECT username FROM user WHERE username = '".$username."' AND password = '".$password."'";
``` 

## Exploit
Como sabemos que a base de dados é SQLite3, usamos para o login admin'-- pois em SQLite3 o comentário é identificado por --. Isto garante-nos o acesso à plataforma, uma vez que salta à frente o processo de verificação da password.
