# Rate Limiting (Limitação de Taxa) para impedir o ataque
O Rate Limiting é uma técnica de defesa de Engenharia de Software e de infraestrutura que controla a taxa (frequência) na qual um usuário, IP ou cliente pode enviar requisições para um serviço, como um formulário de login. Seu objetivo principal é prevenir o Brute Force e ataques de Negação de Serviço (DoS) leves.

### 1. O Conceito
No ataque com o Hydra apresentado, foi enviado centenas (ou milhares) de requisições POST por minuto. O Rate Limiting impede que isso aconteça, limitando o número de tentativas permitidas em um determinado período.

### 2. Implementação e Mecanismos
O Rate Limiting pode ser implementado em diferentes camadas da arquitetura de software:

<table>
  <tr>
    <th>Camada</th>
    <th>Mecanismo de Implementação</th>
    <th>Objetivo</th>
  </tr>
  <tr>
    <td>Aplicação (Código)</td>
    <td>Usando middleware ou lógica de servidor (ex: Python/Flask, Java/Spring). O código verifica um contador armazenado em cache (Redis/Memcached).</td>
    <td>Permite regras mais complexas (ex: bloquear um username específico).</td>
  </tr>
  <tr>
    <td>Infraestrutura (WAF/Proxy)</td>
    <td>Usando um WAF (Web Application Firewall), Balanceador de Carga (ex: Nginx, Cloudflare, AWS WAF).</td>
    <td>Bloqueia requisições antes que cheguem ao servidor da aplicação, economizando recursos.</td>
</table>

### 3. Estratégias Comuns
Para um formulário de login, o Rate Limiting geralmente usa uma destas estratégias:
<ul>
    <li>Por Endereço IP: Limita todas as requisições de login (tentativas bem-sucedidas e falhas) provenientes de um único endereço IP.
        <dt><blockquote>Exemplo: Permitir apenas 5 tentativas de login de um IP a cada 60 segundos.<dt></li>
    <li>Bloqueio por Conta (Account Lockout): Se uma conta específica (admin, no seu caso) receber 3 ou 5 tentativas de senha incorretas em sequência, o sistema bloqueia aquela conta por um período (ex: 15 minutos).</li>
    <li>Delay Exponencial: Em vez de bloquear imediatamente, o sistema introduz um atraso progressivo após cada falha. Após a primeira falha, espera 1 segundo; após a segunda, espera 2 segundos; após a terceira, 4 segundos, e assim por diante. Isso torna o ataque de Força Bruta impraticável e extremamente lento.<dt><blockquote>Um ataque com wordlist de 1000 senhas, que levaria segundos, passaria a levar horas, tornando-o inviável.<dt></li></li>
</ul>

### 4. Conexão com a Perícia Forense
O Rate Limiting é crucial para a Perícia, pois o registro das tentativas de login bloqueadas fornece uma Trilha de Auditoria (Audit Trail). Logs de tentativas repetidas e bloqueios são evidências de que um ataque estava em andamento.