## Progresso do Ataque

O Hydra começou a testar as senhas da wordlist em paralelo, como indicado pelas linhas <code>[ATTEMPT]</code>. Cada tentativa submeteu uma combinação de "admin" com uma senha da lista.

<ul>
<li>Exemplos de tentativas falhas: <code>admin</code> com <code>123456</code>, <code>123456789</code>, <code>iloveyou</code>, entre outras. Para cada uma dessas, o Hydra encontrou a string "Login failed" na resposta do servidor.
</ul>

## Sucesso do Ataque

Na linha <code>[80][HTTP-FORM-POST] host: 192.168.56.101 login: admin password: password</code>, o Hydra reporta o sucesso:

<ul>
<li><strong>Credenciais Encontradas:</strong> A combinação de login: admin e password: password foi identificada como válida. Isso significa que o Hydra enviou essa combinação, e o servidor não retornou a string "Login failed", indicando que o login foi aceito.
<li><strong>Confirmação: </strong>A mensagem <code>1 of 1 target successfully completed, 1 valid password found.</code> valida que o objetivo do ataque foi atingido.
</ul>