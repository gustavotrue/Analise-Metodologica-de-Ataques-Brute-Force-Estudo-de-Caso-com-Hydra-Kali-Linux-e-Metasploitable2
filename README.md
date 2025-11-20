# Análise Metodológica de Ataques Brute Force: Estudo de Caso com Hydra, Kali Linux e Metasploitable2

## 📝 Descrição do Artigo Técnico/Científico

Este repositório documenta um artigo prático de **Hacking Ético** focado na vulnerabilidade de **Autenticação Quebrada (Broken Authentication)**, conforme delineado no OWASP Top 10. O artigo foi desenvolvido com uma visão dupla: a de um atacante (Cibersegurança Junior) e a de um defensor (Engenharia de Software Segura).

O objetivo é realizar uma **Análise Metodológica Detalhada** de um ataque de **Força Bruta (Brute Force)** contra formulários de *login* em uma aplicação web vulnerável.

### Objetivos Específicos

1.  **Perspectiva de Ataque:** Demonstrar o processo de reconhecimento e a execução bem-sucedida de um ataque de Força Bruta utilizando ferramentas padrão da indústria, como **Hydra** no ambiente **Kali Linux**.
2.  **Perspectiva de Defesa (Engenharia de Software):** Propor e discutir contramedidas robustas de **Desenvolvimento Seguro** para mitigar esta vulnerabilidade, incluindo a implementação de *Rate Limiting*, estratégias de bloqueio de conta (*Account Lockout*) e o uso de algoritmos de *Password Hashing* modernos (e.g., Argon2 ou bcrypt).
3.  **Aplicação Prática:** Utilizar o ambiente controlado **Metasploitable2** como alvo para garantir a ética e a segurança da experimentação, aplicando a metodologia de testes de intrusão (`Penetration Testing`).

## ⚙️ Tecnologias Utilizadas

| Categoria | Ferramenta / Tecnologia | Função no Projeto |
| :--- | :--- | :--- |
| **Plataforma de Ataque** | Kali Linux | Sistema operacional para PenTesting. |
| **Alvo Vulnerável** | Metasploitable2 | Máquina virtual intencionalmente vulnerável. |
| **Ferramenta Principal** | Hydra | Execução do ataque de Força Bruta (serviços de rede). |
| **Ferramenta Alternativa** | Burp Suite Community | Interceptação de tráfego e módulo Intruder. |
| **Reconhecimento** | Nmap | Varredura de portas e serviços. |

## 📁 Estrutura do Repositório

O artigo está organizado em fases, seguindo a metodologia padrão de testes de intrusão:

* **`01-SETUP/`**: Documentação sobre a configuração do laboratório virtual (VMs, IPs, rede).
* **`02-SCANNING/`**: Arquivos da fase de reconhecimento, incluindo resultados do Nmap e análise do formulário web alvo.
* **`03-ATTACK/`**: Scripts, comandos exatos (`hydra_command.sh`), wordlists utilizadas e *screenshots* do ataque bem-sucedido.
* **`04-DEFESA_E_CONTRAMEDIDAS/`**: Detalhes sobre a mitigação da vulnerabilidade, com foco nas soluções de Engenharia de Software Segura.
* **`README.md`**: (Este arquivo) Visão geral, objetivos e estrutura do projeto.
* **`LICENSE`**: Arquivo da licença de código aberto (MIT).

## 🚀 Passos para Replicar o Laboratório

1.  **Configuração de VMs:** Instale o Kali Linux e o Metasploitable2 em um hipervisor (VirtualBox/VMware).
2.  **Configuração de Rede:** Garanta que ambas as VMs estejam na mesma rede isolada (*Host-Only* ou *NAT* dedicado).
3.  **Identificação de IPs:** Descubra o endereço IP do Metasploitable2.
4.  **Reconhecimento (Nmap):** Execute uma varredura para identificar o serviço web vulnerável (porta e protocolo).
5.  **Ataque:** Utilize o Hydra ou Burp Suite para submeter tentativas de login automatizadas.

---

## ⚖️ Licença e Aviso Legal

### Licença (MIT)

Este artigo está licenciado sob a **Licença MIT** (veja o arquivo `LICENSE` para detalhes). Você pode usar, copiar, modificar e distribuir este material, desde que o aviso de *copyright* seja mantido.

### ⚠️ Aviso de Isenção de Responsabilidade (Disclaimer)

**Este artigo possui finalidade estritamente acadêmica e educacional (Ethical Hacking).** O conteúdo e os códigos aqui apresentados são destinados **somente** para uso em ambientes de laboratório controlados e com permissão explícita (como o Metasploitable2).

**O autor não se responsabiliza por qualquer uso ilegal, não ético ou malicioso deste material fora de um contexto de teste de intrusão autorizado.** A utilização em sistemas, redes ou aplicações sem consentimento prévio é estritamente proibida e pode resultar em penalidades legais.

***