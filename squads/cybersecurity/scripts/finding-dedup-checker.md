# Finding Dedup Checker

Script para identificar e consolidar findings duplicados em relatorios e trackers de seguranca.

## Descricao

Analisa findings de seguranca e identifica duplicatas ou findings muito similares, permitindo consolidacao e evitando re-trabalho na remediacao.

## Inputs

- `findings_source` - Caminho para arquivo de findings ou conexao com tracker
- `threshold` - Nivel de similaridade para considerar duplicata (padrao: 80%)
- `scope` - Escopo da verificacao (engagement, all)

## Criterios de Deduplicacao

### Match Exato
- Mesma CVE em mesmo asset -> duplicata confirmada
- Mesmo CWE em mesmo endpoint -> provavel duplicata

### Match por Similaridade
- Mesma categoria + mesmo asset + descricao similar -> candidata a dedup
- Mesmo tipo de finding + mesma rede/subnet -> candidata a consolidacao

### Campos Comparados
- CVE ID (se disponivel)
- CWE ID (se disponivel)
- Asset (IP, hostname, URL)
- Tipo de vulnerabilidade
- Severidade
- Descricao (similaridade textual)

## Logica

1. Carregar todos os findings da fonte especificada
2. Normalizar campos para comparacao (lowercase, trim, padronizar IPs)
3. Agrupar findings por CVE ID (match exato)
4. Para findings sem CVE, comparar por CWE + asset
5. Para findings restantes, calcular similaridade textual da descricao
6. Gerar lista de candidatas a duplicata com score de confianca
7. Apresentar para validacao humana

## Output

```
Findings analisados: 87
Duplicatas confirmadas (match exato): 5
Candidatas a dedup (alta confianca): 8
Candidatas a dedup (media confianca): 3

Grupo 1 (CVE-2026-1234):
  - FIND-012: SQL Injection em /api/users (portal-web)
  - FIND-034: SQL Injection em /api/users (portal-web)
  Recomendacao: Consolidar em finding unico

Grupo 2 (similaridade 85%):
  - FIND-015: XSS refletido em search (app-mobile)
  - FIND-028: XSS refletido em busca (app-mobile)
  Recomendacao: Revisar e possivelmente consolidar
```

## Validacoes

- Nunca deletar findings automaticamente, apenas sugerir consolidacao
- Manter registro de todas as deduplicacoes realizadas
- Permitir override manual de sugestoes

## Uso

```
finding-dedup-checker --source findings.json --threshold 80 --scope engagement
```
