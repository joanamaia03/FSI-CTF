# CTF 3

## Desafio 1

- Após algum tempo a explorar o website, encontramos informações pertinentes sobre as versões, plugins instalados e os utilizadores ativos no mesmo:

    Versão do wordpress: 5.8.1

    Plugins instalados e versões:
    - WooCommerce plugin 5.7.1
    - Booster for WooCommerce plugin 5.4.3

    Utilizadores ativos:
    - admin
    - Orval Sanford

- Após procurar o CVE, descobrimos uma vulnerabilidade no Booster for WooComerce plugin, que permite um atacante inicar sessão como um utilizador comum. O CVE encontrado encontrado foi o CVE-2021-34646, com um score crítico de 9.8.

Flag: flag{CVE-2021-34646}

## Desafio 2

- Após alguma pesquisa deste CVE, descobrimos um exploit no website https://www.exploit-db.com/exploits/50299. 

- Correndo o mesmo e utilizando como argumentos o url ( http://ctf-fsi.fe.up.pt:5001) e o id=1 (corresponde ao admin pois é a primeira conta a ser criada na base de dados), são gerados 3 links que podem ser utilizados para iniciar sessão como administrador.

- No entanto, apenas um destes links (http://ctf-fsi.fe.up.pt:5001/wp-admin/edit.php) nos permite aceder a ao ficheiro onde se encontra a flag necessária.

Flag: flag{"please don't bother me"}


