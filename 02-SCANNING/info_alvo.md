## Informações do alvo
Endereço IP:                          192.168.56.101
Porta Alvo:                           80 (Identificada pelo Nmap)
Serviço:                              HTTP (Apache httpd 2.2.8 ((Ubuntu) DAV/2))
Aplicação Alvo:                       Damn Vulnerable Web Application (DVWA)
URL Completa do Formulário:           http://192.168.56.101/dvwa/login.php

---

### Justificativa de Reconhecimento da Aplicação DVWA

Este segmento documenta o processo de identificação da aplicação web alvo, fazendo uma distinção entre a metodologia de *scanning* de rede e a de *Application Fingerprinting*.

### 1. Foco do Nmap (Scanning de Rede)

O comando **Nmap** (`nmap -p- -sV 192.168.56.101`) tem como objetivo primário identificar o **endereço IP** do alvo e mapear as **portas e serviços** abertos.

* **Resultado:** O Nmap confirmou que a **Porta 80** estava aberta, indicando a presença de um servidor **HTTP** (Servidor Web Apache).
* **Limitação:** O Nmap, por si só, não especifica o software de aplicação (como DVWA, WordPress ou Joomla) que está sendo executado sobre o servidor web.

### 2. Confirmação do Alvo (Contexto Acadêmico)

A identificação da aplicação **DVWA** (Damn Vulnerable Web Application) foi realizada através da aplicação do **Conhecimento Prévio do Laboratório**, o que é uma prática comum e aceitável em ambientes controlados:

* **Metasploitable2:** É uma máquina virtual intencionalmente vulnerável, cujo propósito é hospedar aplicações-alvo como o DVWA.
* **Acesso Direto (Análise Manual):** Após a confirmação da Porta 80 aberta, o acesso direto ao IP no navegador (`http://192.168.56.101/`) revela o índice do servidor, onde o diretório `/dvwa` e o formulário de login (`login.php`) são facilmente localizados.

### 3. Rigor Metodológico

Para fins de um **Penetration Test** real e desconhecido, a confirmação do DVWA seria realizada através de técnicas de **Impressão Digital de Aplicação (Application Fingerprinting)** mais sofisticadas (como a análise de *headers*, *cookies* ou o uso de ferramentas como o **WhatWeb**).

Neste projeto acadêmico, a confirmação rápida do DVWA permite que o foco seja mantido na análise dos parâmetros do formulário e na execução metodológica do **Ataque de Força Bruta**, seguido pela discussão aprofundada das **Contramedidas de Engenharia de Software**.

---