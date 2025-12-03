# Desafio_Final_Modulo3

# 🛡️ TechCorp Solutions – Relatório de Teste de Intrusão (Pentest)

**Autor:** Gonçalo Quissola Dala  
**Data do Teste:** 19–27 de Novembro de 2025  
**Versão:** 1.0  
**Método:** OWASP + PTES  
**Tipo de Teste:** Black Box Testing  
**Ambiente CTF:** http://98.95.207.28/

---

## 📌 1. Descrição do Projeto

Este repositório contém o relatório profissional do Pentest realizado no ambiente da **TechCorp Solutions**, como parte do Desafio Final do Módulo 3.  
Foram identificadas vulnerabilidades críticas que comprometem severamente a segurança do sistema.

---

## 📌 2. Objetivos do Pentest

- Identificar vulnerabilidades em serviços expostos  
- Avaliar a segurança do servidor web e FTP  
- Testar resistência contra SQLi, XSS, LFI  
- Localizar arquivos, credenciais e diretórios sensíveis  
- Validar mecanismos de autenticação  
- Capturar flags distribuídas pelo sistema  
- Produzir relatório técnico e executivo  

---

## 📌 3. Escopo

### **Sistemas incluídos**
- Servidor Web: **98.95.207.28:80**
- Servidor FTP: **98.95.207.28:21**
- Banco de Dados MySQL
- Painéis administrativos
- Diretórios acessíveis publicamente

### **Limitações**
- Janelas de teste: **22:00–06:00**
- Sem DoS/DDoS  
- Sem engenharia social  

---

## 📌 4. Flags Capturadas

### **⚠️ Flags de Credenciais Expostas**
| Flag | Localização | Descrição |
|------|-------------|-----------|
| `FLAG{p4ssw@rd_f113_disc0v3ry}` | passwords.txt | Senhas corporativas expostas |
| `FLAG{git_cr3d3nt1418_134k}` | /.git-credentials | Token GitHub exposto |
| `FLAG{d4t4b4s3_cr3d3nt141s_3xp0s3d}` | config/database.php.txt | Credenciais do BD públicas |

### **⚠️ Flags de Acesso e Descoberta**
| Flag | Local | Descrição |
|------|-------|-----------|
| `FLAG{ftp_4n6nym0us_4cc3ss}` | FTP | FTP anônimo ativo |
| `FLAG{s3cr3t_p4n3l_disc0v3ry}` | /panel.php | Painel administrativo exposto |
| `FLAG{c0nfig_fil3_r34d}` | users.conf | Arquivo de config exposto |
| `FLAG{h1dd3n_d4t4_1n_d4t4b4s3}` | Banco de Dados | Dados ocultos encontrados |
| `FLAG{sql_1nj3ct10n_m4st3r}` | Parâmetros | SQL Injection |
| `FLAG{d4t4b4s3_1nj3ct10n_m4st3r}` | Formulário login | Bypass via SQLi |

### **⚠️ Flags de Vulnerabilidades**
| Flag | Tipo |
|------|------|
| `FLAG{b4sic_s0urc3_c0d3_insp3cti0n}` | Comentários no código expostos |
| `FLAG{lfi_vuln3r4b1lity}` | Local File Inclusion |
| `FLAG{xss_r3fl3ct3d_vuln3r4b1l1ty}` | XSS refletido |

---

## 📌 5. Vulnerabilidades Identificadas

### 🔥 **Críticas**
- **Exposição de credenciais** em passwords.txt, .git-credentials, database.php.txt  
- **FTP anônimo** habilitado  
- **Injeção SQL** em múltiplos endpoints  

### ⚠️ **Altas**
- XSS refletido  
- LFI via parâmetro `file` em /panel.php  
- Enumeração de diretórios sensíveis  

### ⚙️ **Médias/Baixas**
- Informações do sistema expostas  
- Diretórios indexáveis  
- Estrutura do BD sem controle de acesso  

---

## 📌 6. Metodologia

### 🔍 **Reconhecimento**
Ferramentas:
- Nmap  
- Gobuster  
- Dirb  

Serviços encontrados:
- Apache/PHP (porta 80)
- vsFTPd 3.0.5 (porta 21)
- MySQL (3306)
- SSH alternativo (2222)

### 📡 **Varredura**
- SQLmap  
- Nmap NSE  
- Enumeração manual  

### 🎯 **Exploração**
- Acesso FTP anônimo  
- SQL Injection (bypass e extração de dados)  
- LFI em `/panel.php?file=`  
- Coleta de arquivos sensíveis  

### 📥 **Pós-Exploração**
- Extração de credenciais  
- Leitura de backups  
- Coleta de evidências  
- Validação de impacto  

---

## 📌 7. Evidências Coletadas

### **7.1 Credenciais Reais Encontradas**
(Do PDF)

passwords.txt

SSH: techcorp:TechCorp2024!
FTP Admin: ftpadmin:ftp@dmin123
Database: backup_user:B@cKup_S3cr3t_2024
WiFi: TechCorp_WiFi_2024
VPN: vpn_user:VPN_P@ssw@rd/

.git-credentials
https://admin:gh_pkt_53cr3tT0k3n_2024_TechCorp@github.com

database.php
$db_user = 'techcorp_user';
$db_pass = 'TechCorp_DB_P@ss_2024!';

### **7.2 Configurações Vulneráveis**

vsFTPd - Anonymous login enabled
Apache - Directory listing enabled
PHP - Error reporting enabled
MySQL - Excessive permissions

---

## 📌 8. Recomendações

### 🟥 **Ações Imediatas (24–48h)**
- Desabilitar FTP anônimo  
- Remover arquivos sensíveis  
- Corrigir SQL Injection  
- Alterar todas as senhas expostas  
- Aplicar restrições a diretórios  

### 🟧 **Médio Prazo (1–2 semanas)**
- Implementar gestão de segredos  
- Configurar WAF  
- Corrigir XSS e LFI  
- Melhorar permissões MySQL  

### 🟩 **Longo Prazo (1 mês)**
- Implementar SDLC seguro  
- Adoção de RBAC  
- Auditorias regulares  
- Treinamento da equipe  

---

## 📌 9. Conclusão

O ambiente analisado mostrou vulnerabilidades graves que possibilitaram:

- Comprometimento total do servidor  
- Acesso a credenciais sensíveis  
- Extração completa do banco de dados  
- Contorno de autenticação  

📌 **Status Final: INSEGURO**

Recomenda-se aplicar imediatamente as ações listadas e realizar um reteste formal.

---

## 📎 10. Estrutura do Repositório

/
├── README.md # Este arquivo
├── Relatorio_Pentest.docx # Relatório profissional
├── evidencias/ # Capturas de tela e arquivos coletados
├── logs/ # logs de terminal, nmap, sqlmap
├── flags/ # Registro das flags capturadas

---

## 📄 11. Licença

Uso autorizado exclusivamente para fins acadêmicos.  
TechCorp Solutions — Ambiente CTF.
