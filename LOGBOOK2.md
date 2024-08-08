# Trabalho realizado nas Semanas #2 e #3

## Identificação

- CVE-2017-11882 é uma vulnerabilidade de execução remota de código não arbitrário no Microsoft Office.
- É originada do executável Equation Editor, que apresenta uma vulnerabilidade de Stack Buffer Overflow.
- O Equation Editor (eqnedt32.exe) fazia uso do Component Object Model (COM), causando uma falha na proteção contra a vulnerabilidade por parte do EMET e do Windows Defender Exploit Guard.
- Afetou várias versões do Microsoft Office no Windows 7, 8 e 10, sendo as versões anteriores ao Windows 8.0 mais suscetíveis à vulnerabilidade, devido à configuração ASLR (Address Space Layout Randomization) padrão.

## Catalogação

- A CVE-2017-11882 foi relatada em novembro de 2017 pela empresa de segurança FireEye. 
- Não foram identificadas informações sobre um programa de recompensa por falhas relacionadas a esta vulnerabilidade. 
- A classificação como "gravidade alta" deve-se ao seu potencial impacto na segurança do Microsoft Office e do sistema operacional Windows, para além de afetar os seus usuários, que eram centenas de milhões na época.

## Exploração da Vulnerabilidade

- A vulnerabilidade começa por ser explorada através da criação de um documento Office, como um arquivo do Word (.doc) ou Excel (.xls), que contém um arquivo RTF malicioso.
- Esse arquivo RTF contém instruções que exploram o Buffer Overflow, para executar código arbitrário.
- Quando um documento contendo o arquivo RTF é aberto, o código malicioso é executado sem a necessidade de interação por parte do usuário, por via do Equation Editor.

## Ataques

- Em 2017, uma prova de conceito (PoC) surgiu na internet e os ataques que usavam a CVE-2017-11882 começaram logo em seguida.
- Em 2020, durante a pandemia de Covid-19, a CVE-2017-11882 foi usada ativamente em correspondências maliciosas que usavam como contexto a interrupção das logísticas de entregas devido a restrições sanitárias.
- Em 2022, a CVE-2017-11882 foi utilizada para atacar mais de 487.000 utilizadores, através de versões mais antigas de programas provenientes do Microsoft Office.
