# OPSEC Guidelines

Diretrizes de seguranca operacional para membros do Cybersecurity Squad.

## Principio Central

A equipe de seguranca deve ser exemplar na protecao de suas proprias operacoes. Informacoes sobre vulnerabilidades, tecnicas e ferramentas do squad sao altamente sensiveis.

## Classificacao de Informacoes do Squad

### Confidencial
- Relatorios de pentest com vulnerabilidades ativas
- Exploits e payloads customizados
- Credenciais obtidas durante testes
- Detalhes de detection rules e gaps de cobertura

### Restrito
- Planejamento de exercicios de seguranca
- Arquitetura de seguranca e controles implementados
- Metricas detalhadas de seguranca
- Detalhes de incidentes em investigacao

### Interno
- Politicas e procedimentos de seguranca
- Checklists e templates genericos
- Metricas agregadas e sanitizadas

## Comunicacao Segura

- Findings de seguranca devem ser compartilhados apenas por canais aprovados e criptografados
- Nunca discutir vulnerabilidades ativas em canais publicos ou nao-criptografados
- Evidencias de pentest nao devem ser enviadas por email sem criptografia
- Screenshots com dados sensiveis devem ser redactados antes de compartilhar

## Gestao de Credenciais

- Credenciais do squad devem ser armazenadas exclusivamente em password manager aprovado
- Credenciais de teste devem ser unicas por engagement e descartadas apos conclusao
- MFA e obrigatorio para todos os sistemas utilizados pelo squad
- Service accounts devem ter permissoes minimas e rotacao periodica

## Ferramentas e Infraestrutura

- Ferramentas ofensivas devem ser mantidas em ambiente isolado e controlado
- Atualizacoes de ferramentas devem ser validadas antes de uso em engagements
- Payloads e exploits customizados nao devem ser publicados externamente
- Infraestrutura de teste (C2, proxies) deve ser descartada apos cada engagement

## Protecao de Evidencias

- Evidencias devem ser armazenadas em repositorio seguro com controle de acesso
- Hash de integridade deve ser gerado para cada evidencia coletada
- Chain of custody deve ser mantida para evidencias com potencial uso juridico
- Descarte de evidencias deve seguir procedimento documentado

## Redes e Acessos

- Testes ofensivos devem partir de redes e maquinas designadas
- VPN do squad deve ser usada para todo acesso remoto
- Acesso a ambientes de producao requer justificativa e aprovacao
- Logs de acesso do squad devem ser preservados para auditoria

## Viagem e Trabalho Remoto

- Equipamentos do squad devem ter full disk encryption
- Conexoes publicas de internet requerem uso de VPN
- Nunca deixar equipamentos desbloqueados sem supervisao
- Materiais sensiveis nao devem ser exibidos em locais publicos

## Violacoes de OPSEC

- Reportar imediatamente qualquer violacao ou suspeita ao squad lead
- Violacoes serao tratadas como incidentes de seguranca
- Analise de impacto deve ser conduzida para cada violacao
- Acoes corretivas devem ser implementadas e documentadas
