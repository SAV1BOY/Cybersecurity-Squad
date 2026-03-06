# Credential Attack Methodology

## Aviso Legal
> Este documento destina-se exclusivamente a testes de seguranca AUTORIZADOS.
> Qualquer uso sem autorizacao formal e expressa e ilegal e antiético.

## Visao Geral
Metodologia aplicada para avaliacao de resiliencia de credenciais em ambientes corporativos.
Abrange ataques baseados em senhas, tickets Kerberos e reutilizacao de hashes.
Todos os testes exigem autorizacao por escrito do proprietario do ambiente.

## Requisitos de Autorizacao
- Contrato de pentest assinado com escopo definido (Rules of Engagement)
- Aprovacao formal do CISO ou responsavel pelo ambiente
- Lista de alvos autorizados (IP ranges, dominios, contas de teste)
- Clausula de confidencialidade e tratamento de dados sensiveis
- Plano de rollback e contato de emergencia definidos

## Etapas da Metodologia

### 1. Reconhecimento de Credenciais
- Enumeracao de politicas de senha via LDAP queries
- Identificacao de lockout threshold e password complexity requirements
- Coleta de usernames validos por meio de RPC enumeration e OSINT

### 2. Password Spraying
- Selecao de senhas comuns respeitando lockout policies
- Execucao controlada com intervalos para evitar account lockout
- Monitoramento de respostas para identificar credenciais validas
- Registro detalhado de tentativas para auditoria

### 3. Credential Stuffing
- Utilizacao de listas de credenciais vazadas (breach databases)
- Correlacao de emails corporativos com dados publicos de vazamentos
- Teste automatizado contra portais de autenticacao autorizados

### 4. Kerberoasting
- Solicitacao de TGS tickets para contas com servicePrincipalName
- Extracao de tickets para cracking offline
- Identificacao de contas de servico com senhas fracas
- Priorizacao de contas com privilegios elevados

### 5. AS-REP Roasting
- Identificacao de contas com DONT_REQUIRE_PREAUTH habilitado
- Solicitacao de AS-REP sem pre-autenticacao
- Extracao e cracking offline dos hashes resultantes

### 6. Pass-the-Hash (PtH)
- Extracao de NTLM hashes da memoria (requer privilegio local)
- Reutilizacao de hashes para autenticacao em sistemas autorizados
- Validacao de movimentacao lateral possivel com credenciais obtidas

## Ferramentas de Referencia
- Hydra, Burp Suite, CrackMapExec, Rubeus, Impacket, Hashcat, Mimikatz
- Observacao: uso exclusivo em ambientes autorizados com versoes auditadas

## Contrapartida de Deteccao (Blue Team)
- Monitoramento de Event ID 4625 (failed logons) e 4771 (Kerberos pre-auth failure)
- Alertas para volume anomalo de TGS requests (Kerberoasting indicator)
- Deteccao de PtH via Event ID 4624 com logon type 9 (NewCredentials)
- Correlacao de spray patterns: muitas contas, poucas senhas, curto intervalo
- Auditoria de contas com DONT_REQUIRE_PREAUTH via AD queries periodicas

## Integracao com Outros Frameworks
- Alimenta: lateral-movement-methodology.md (credenciais obtidas)
- Alimenta: privilege-escalation-methodology.md (contas de servico)
- Recebe de: active-directory-attack-defense.md (enumeracao AD)
- Reporta para: SIEM e plataforma de gestao de vulnerabilidades
