# Detection Coverage Calculator

Script para calcular e visualizar a cobertura de deteccao contra o framework MITRE ATT&CK.

## Descricao

Mapeia as detection rules existentes ao ATT&CK e calcula metricas de cobertura por tactic, technique e data source, gerando heat map de visibilidade.

## Inputs

- `rules_inventory` - Arquivo com inventario de detection rules e seus mapeamentos ATT&CK
- `attack_matrix` - Versao do ATT&CK a utilizar (ex: v14)
- `priority_techniques` - Lista de tecnicas prioritarias para o ambiente
- `output_format` - Formato de saida (json, csv, navigator_layer)

## Logica

1. Carregar inventario de detection rules com mapeamentos ATT&CK
2. Carregar a matriz ATT&CK na versao especificada
3. Para cada technique na matriz:
   - Verificar se existe pelo menos uma rule mapeada
   - Contar numero de rules por technique
   - Verificar se as rules estao ativas e eficazes
4. Calcular metricas por tactic e geral
5. Destacar tecnicas prioritarias sem cobertura
6. Gerar output no formato solicitado

## Metricas Calculadas

- Cobertura geral: % de techniques com pelo menos uma rule
- Cobertura por tactic: % dentro de cada tactic
- Cobertura prioritaria: % das techniques prioritarias cobertas
- Profundidade: numero medio de rules por technique coberta
- Gaps criticos: techniques prioritarias sem cobertura

## Output

```
Cobertura Geral: 47% (89 de 190 techniques)
Cobertura Prioritaria: 62% (31 de 50 techniques)

Por Tactic:
  Initial Access:    55% (6/11)
  Execution:         70% (7/10)
  Persistence:       40% (6/15)
  Privilege Escalation: 35% (5/14)
  Defense Evasion:   25% (6/24)
  ...

Gaps Prioritarios (sem cobertura):
  T1055 - Process Injection
  T1218 - System Binary Proxy Execution
  T1562 - Impair Defenses
  ...
```

## Integracao com ATT&CK Navigator

Gera arquivo JSON no formato ATT&CK Navigator layer para visualizacao no heat map, com cores indicando nivel de cobertura por technique.

## Uso

```
detection-coverage-calculator --rules rules.json --matrix v14 --priority priority.txt --output navigator_layer
```
