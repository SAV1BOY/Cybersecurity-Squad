# Reporting Standards

Padroes de qualidade e consistencia para todos os relatorios produzidos pelo Cybersecurity Squad.

## Principios de Reporting

1. **Precisao** - Toda afirmacao deve ser verificavel e baseada em evidencia
2. **Clareza** - Linguagem acessivel para a audiencia-alvo
3. **Consistencia** - Mesma estrutura e terminologia em todos os relatorios
4. **Acionabilidade** - Recomendacoes devem ser praticas e implementaveis
5. **Rastreabilidade** - Findings devem ser rastreaveis ate a evidencia de origem

## Estrutura Padrao de Relatorio

### Elementos Obrigatorios
- Capa com titulo, data, classificacao e versao
- Executive summary (maximo 1 pagina)
- Escopo e metodologia
- Findings detalhados com evidencias
- Recomendacoes priorizadas
- Apendices com dados complementares

### Formatacao
- Usar templates aprovados do squad
- Numeracao sequencial de paginas
- Indice para relatorios com mais de 10 paginas
- Classificacao de confidencialidade em todas as paginas

## Classificacao de Findings

### Escala de Severidade
- **Critical** - CVSS 9.0-10.0, exploracao trivial, impacto maximo
- **High** - CVSS 7.0-8.9, exploracao possivel, impacto significativo
- **Medium** - CVSS 4.0-6.9, exploracao com condicoes, impacto moderado
- **Low** - CVSS 0.1-3.9, exploracao dificil, impacto limitado
- **Informational** - Sem CVSS, observacao sem impacto direto

### Estrutura de Finding
Cada finding deve conter obrigatoriamente:
- ID unico do finding
- Titulo descritivo
- Severidade com justificativa
- Descricao tecnica detalhada
- Evidencia (screenshot, log, output)
- Impacto ao negocio
- Recomendacao de remediacao
- Referencia (CVE, CWE, OWASP, etc)

## Qualidade de Evidencia

- Screenshots devem estar legíveis e com areas relevantes destacadas
- Comandos executados devem ser reproduziveis
- Timestamps devem estar em UTC
- Dados sensiveis devem ser redactados (exceto o necessario para comprovar o finding)

## Revisao e Aprovacao

- Todo relatorio passa por peer review antes da entrega
- Reviewer verifica: precisao tecnica, clareza, completude, formatacao
- Findings criticos devem ter revisao por senior analyst
- Relatorio final requer aprovacao do engagement lead

## Prazos de Entrega

- Draft para review interno: ate 5 dias uteis apos conclusao dos testes
- Relatorio final: ate 3 dias uteis apos aprovacao do review
- Findings criticos: notificacao verbal imediata, seguida de report escrito em 24h

## Retencao e Distribuicao

- Relatorios sao classificados como confidenciais por padrao
- Distribuicao limitada ao cliente e stakeholders autorizados
- Retencao conforme politica organizacional (minimo 3 anos)
- Descarte seguro apos periodo de retencao
