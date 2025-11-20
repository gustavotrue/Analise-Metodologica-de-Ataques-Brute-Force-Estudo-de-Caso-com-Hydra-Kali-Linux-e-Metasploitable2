## Password Hashing Seguro para proteger os dados em caso de falha
O Hashing de senhas é o processo de transformar a senha de texto puro (plaintext) em uma string de tamanho fixo e ilegível, chamada hash. A característica mais importante de uma função de hashing segura é que ela deve ser uma função unidirecional: é fácil calcular o hash a partir da senha, mas é computacionalmente inviável fazer o caminho inverso.

### 1. Por que é Indispensável?
O objetivo principal é proteger as senhas em repouso (armazenadas no banco de dados).

<ul>
<li><strong>Vazamento de Dados:</strong> Se um atacante (ou um perito forense) conseguir acesso não autorizado ao banco de dados (ex: por meio de um ataque de Injeção de SQL), ele encontrará apenas os hashes, e não as senhas reais.

<li><strong>Prevenção de Ataques Off-line:</strong> Um hash forte resiste a ataques off-line, como a <strong>Força Bruta</strong> ou <strong>Rainbow Tables</strong>, que tentam adivinhar a senha real comparando-a com hashes pré-calculados.
</ul>

### 2. Funções de Hashing Modernas (Recomendadas)
Em <strong>Engenharia de Software</strong> moderna, é <strong>vital</strong> evitar funções rápidas e antigas como <strong>MD5</strong> e <strong>SHA-1</strong> (que são vulneráveis a Rainbow Tables e ataques de colisão). As funções recomendadas atualmente são aquelas projetadas intencionalmente para serem <strong>lentas</strong> e <strong>custosas em termos de CPU/Memória:</strong>

<ul>
<li><strong>Argon2:</strong> Atualmente, é o algoritmo mais recomendado (vencedor da Password Hashing Competition). Oferece resistência contra ataques de Força Bruta baseados em GPU e ataques paralelos, pois permite configurar o uso de memória e CPU.
<li><strong>bcrypt:</strong> Amplamente adotado e considerado um padrão de mercado por muitos anos. Usa um fator de custo que pode ser aumentado ao longo do tempo para acompanhar o aumento da capacidade de processamento dos atacantes.
<li><strong>scrypt:</strong> Semelhante ao Argon2, permite configurar o consumo de memória, tornando a Força Bruta mais cara.
</ul>

### 3. O Conceito de Salting (Salgamento)
Independentemente da função escolhida, a senha deve ser "salgada":
<ul>
<li><strong>Salt (Sal):</strong> É uma string de dados aleatória e única que é adicionada à senha antes de ser hasheada.
<li><strong>Função:</strong> Garante que senhas iguais (ex: "123456") terão hashes totalmente diferentes no banco de dados. Isso frustra os ataques de Rainbow Table e evita que um atacante descubra instantaneamente todos os usuários que usam a mesma senha.
</ul>