# Asset Inventory Diff

Script para comparar snapshots do inventario de assets e identificar mudancas.

## Descricao

Compara dois snapshots do asset inventory para identificar novos assets, assets removidos e mudancas em configuracao, ajudando a manter visibilidade sobre a attack surface.

## Inputs

- `baseline` - Snapshot anterior do inventario (arquivo JSON ou CSV)
- `current` - Snapshot atual do inventario
- `ignore_fields` - Campos a ignorar na comparacao (ex: last_seen)

## Campos Comparados

- IP address e hostname
- Portas e servicos expostos
- Sistema operacional e versao
- Owner e classificacao de criticidade
- Status (ativo, inativo, descomissionado)

## Logica

1. Carregar ambos os snapshots e normalizar formatos
2. Identificar assets presentes apenas no current (novos)
3. Identificar assets presentes apenas no baseline (removidos)
4. Para assets presentes em ambos:
   - Comparar cada campo (exceto ignored)
   - Registrar diferencas encontradas
5. Classificar mudancas por tipo e risco
6. Gerar relatorio de diff

## Output

```
Asset Inventory Diff Report
Baseline: 2026-02-01 (342 assets)
Current: 2026-03-01 (356 assets)

Novos assets: 18
  + 10.0.1.50 (web-server-new) - Portas: 80, 443
  + 10.0.2.71 (db-replica-03) - Portas: 5432
  ...

Assets removidos: 4
  - 10.0.1.22 (legacy-app) - Ultima vez: 2026-02-15
  ...

Assets modificados: 12
  ~ 10.0.1.10: Nova porta aberta 8080 (era: 80, 443)
  ~ 10.0.3.5: OS atualizado de Ubuntu 20.04 para 22.04
  ...

Alertas:
  [HIGH] 3 novos assets sem owner definido
  [HIGH] 2 novos assets com portas de admin expostas
  [MEDIUM] 1 asset mudou de rede interna para DMZ
```

## Alertas Automaticos

- Novo asset sem owner -> alerta para asset management
- Nova porta exposta em asset critico -> alerta para security team
- Asset critico removido sem registro -> alerta para investigacao

## Uso

```
asset-inventory-diff --baseline inventory-2026-02.json --current inventory-2026-03.json
```

## Agendamento

Recomendado executar semanalmente ou apos cada scan de descoberta para manter visibilidade atualizada.
