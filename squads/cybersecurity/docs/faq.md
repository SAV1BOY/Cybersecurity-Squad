# FAQ

Perguntas frequentes sobre o Cybersecurity Squad e seus processos.

## Geral

### Como solicito uma avaliacao de seguranca?
Preencha o formulario de intake disponivel no canal do squad. A triagem sera feita em ate 2 dias uteis e voce recebera confirmacao com timeline estimado.

### Qual a diferenca entre pentest e vulnerability scan?
Vulnerability scan e automatizado e identifica vulnerabilidades conhecidas. Pentest e manual e simulacao de ataque real, incluindo exploracao e avaliacao de impacto. O pentest vai alem do scan.

### Como reporto um incidente de seguranca?
Use o canal de emergencia do squad. Para incidentes P1/P2, o SLA de resposta e de 15 minutos. Inclua o maximo de informacao possivel no reporte inicial.

### Preciso de autorizacao para fazer um pentest?
Sim, sempre. Nenhum teste de seguranca deve ser executado sem authorization letter assinada. Consulte legal-and-authorization.md para detalhes.

## Workflows

### Posso adaptar um workflow ao meu contexto?
Sim, desde que mantenha o objetivo original, respeite os decision points criticos e documente os desvios. Consulte workflow-guide.md para diretrizes.

### Qual workflow usar para avaliar um novo sistema?
Use o new-system-security-review-workflow.md. Ele cobre todo o processo desde o intake ate o monitoramento pos-launch.

### Como funciona o handoff entre squads?
Siga o cross-squad-handoff-workflow.md. O processo garante que contexto, responsabilidades e artefatos sejam transferidos de forma estruturada.

## Findings e Remediacao

### Quais sao os SLAs de remediacao?
- Critical: 48 horas (emergencia)
- High: 15 dias uteis
- Medium: 30 dias uteis
- Low: 90 dias uteis
- Informational: sem SLA obrigatorio

### Posso solicitar risk acceptance?
Sim, desde que a justificativa seja documentada e aprovada pelo nivel de autoridade adequado conforme a politica. Consulte risk-acceptance-phrases.md para linguagem padrao.

### O que acontece se o SLA for violado?
O finding e escalado para management do owner conforme o processo de escalacao. Consulte escalation-phrases.md para comunicacoes padrao.

## Metricas e Reporting

### Com que frequencia sao publicadas metricas?
Metricas operacionais sao atualizadas semanalmente no dashboard. Relatorios formais sao publicados mensalmente e a revisao estrategica e trimestral.

### Onde encontro os dashboards de seguranca?
Os dashboards estao disponiveis na plataforma de BI com acesso controlado. Solicite acesso via canal do squad se nao tiver.

## Onboarding

### Quanto tempo leva o onboarding completo?
O processo formal de onboarding dura 4 semanas, conforme descrito em onboarding.md. A autonomia completa geralmente e atingida em 60-90 dias.

### Quem e meu buddy de onboarding?
Seu buddy sera designado pelo squad lead no primeiro dia. O buddy e seu ponto de contato principal durante as primeiras semanas.

## Ferramentas

### Quais ferramentas o squad utiliza?
A lista completa de ferramentas e disponibilizada durante o onboarding. As principais categorias incluem SIEM, vulnerability scanners, ferramentas ofensivas e plataformas de tracking.

### Posso usar ferramentas nao aprovadas?
Nao em engagements oficiais. Novas ferramentas devem ser avaliadas e aprovadas antes do uso. Consulte opsec-guidelines.md para diretrizes.
