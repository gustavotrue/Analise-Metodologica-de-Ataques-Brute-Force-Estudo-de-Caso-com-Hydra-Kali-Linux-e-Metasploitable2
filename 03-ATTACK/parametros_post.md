## Análise e Uso dos Parâmetros POST no Hydra
Para que o ataque de Força Bruta seja eficaz, a ferramenta Hydra deve imitar perfeitamente o navegador, enviando os dados de login de forma que o servidor web os aceite. Isso é feito através dos Parâmetros POST.

### 1. O Papel da Requisição HTTP POST
Um formulário de login utiliza o método HTTP POST para enviar dados ao servidor. A informação não é passada pela URL (como no GET), mas sim no corpo da requisição. O Hydra precisa que esses dados sejam estruturados exatamente como o servidor espera.
<ul>
    <li>Identificação: Os nomes exatos dos campos (username, password, Login) são descobertos através da inspeção do código-fonte HTML do formulário ou da captura da requisição real usando um proxy (como o Burp Suite).</li>
</ul>

### 2. Mapeamento de Parâmetros para o Hydra
O comando Hydra usa o switch http-post-form para definir a string exata dos parâmetros. Para o formulário do DVWA, a string capturada é:

<p><code>username=USER_INPUT&password=PASSWORD_INPUT&Login=Login</code></p>

O Hydra traduz essa string da seguinte forma:

<table>
  <tr>
    <th>Parâmetro no Formulário</th>
    <th>Variável no Hydra</th>
    <th>Função</th>
  </tr>
  <tr>
    <td><code>username=</code></td>
    <td><code>^USER^</code></td>
    <td>Um placeholder (marcador de posição) onde o Hydra insere cada nome de usuário testado (ou o nome de usuário fixo definido com <code>-l</code>).</td>
  </tr>
  <tr>
    <td><code>password=</code></td>
    <td><code>^PASS^</code></td>
    <td>O placeholder onde o Hydra insere cada senha da wordlist (definida com <code>-P</code>).</td>
  </tr><tr>
    <td><code>&Login=Login</code></td>
    <td>Literal</td>
    <td>É o campo do botão de submissão do formulário. Ele deve ser incluído exatamente como aparece na requisição POST para que o servidor processe o login corretamente.</td>
  </tr>
</table>

### 3. A Lógica de Sucesso e Falha

O comando completo passado ao Hydra é:

<code>hydra -l admin -P /home/kali/LabG/Wordlist-Users/rockyou.txt 192.168.56.101 http-post-form "/dvwa/login.php:username=^USER^&password=^PASS^&Login=Login:F=Login failed" -V</code>

O Hydra insere a combinação de <code>^USER^</code> e <code>^PASS^</code> no corpo da requisição e a envia ao servidor. Em seguida, ele analisa a resposta do servidor:
<ul>
    <li>Falha (Failed): Se o servidor retornar uma página que contenha a frase Login failed, o Hydra descarta a tentativa e avança para a próxima senha.</li>
    <li>Sucesso (Success): Se o servidor retornar uma página sem a frase Login failed (indicando um redirecionamento ou a página de login interno), o Hydra assume que as credenciais são válidas e as registra.</li>
</ul>

> Dessa forma, o Hydra não precisa de um navegador; ele utiliza os parâmetros POST para se comunicar diretamente no nível de Protocolo HTTP, que é a linguagem que o servidor web entende.
