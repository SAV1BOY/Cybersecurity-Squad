# Security Champion Program — Framework Interno

> Como escalar seguranca atraves de developers embedded em cada time.

## Objetivo

Security champions sao developers que recebem treinamento adicional em seguranca e servem como ponto de contato entre o time de desenvolvimento e o squad de seguranca. Eles nao substituem o squad — eles multiplicam o alcance.

## Modelo

### Papel do Champion
- **Nao e**: Security expert, auditor, bloqueador de deploys
- **E**: Developer com consciencia de seguranca, primeiro ponto de contato, facilitador

### Responsabilidades
1. Participar de threat modeling sessions do seu projeto
2. Revisar PRs com foco em seguranca (checklist basico)
3. Escalar duvidas de seguranca para o squad
4. Participar de treinamento mensal de seguranca
5. Disseminar boas praticas no time
6. Reportar riscos e preocupacoes de seguranca

### O que NAO e responsabilidade do champion
- Fazer pentest
- Tomar decisoes de risco de negocio
- Ser o unico responsavel por seguranca do projeto
- Bloquear releases sem backing do squad

## Programa

### Onboarding (2 semanas)
1. Workshop de OWASP Top 10 (pratico, com lab)
2. Threat modeling basico (STRIDE simplificado)
3. Secure coding na linguagem do time
4. Ferramentas de seguranca do CI/CD pipeline
5. Como escalar para o squad

### Treinamento Continuo (mensal)
- 1 sessao de 1h por mes
- Topicos rotativos: auth, crypto, injection, API security, cloud security
- Formato: 30 min teoria + 30 min hands-on/CTF
- Material disponivel em reference/

### Cadencia
| Frequencia | Atividade |
|------------|-----------|
| Semanal | PR review com foco em seguranca |
| Quinzenal | Office hours com o squad |
| Mensal | Training session |
| Trimestral | Threat model review do projeto |
| Semestral | Assessment do programa |

## Metricas do Programa

- % de dev teams com champion ativo
- Numero de escalacoes ao squad (mais = melhor awareness)
- Vulns encontradas por champions vs. pelo squad
- Participacao nos treinamentos
- NPS do programa (champions gostam de participar?)

## Agentes Envolvidos

- **Jim Manico**: Conteudo tecnico, treinamento, mentoria
- **Marcus Carey**: Cultura, engajamento, comunicacao
- **Cyber Chief**: Estrategia e cobertura do programa
