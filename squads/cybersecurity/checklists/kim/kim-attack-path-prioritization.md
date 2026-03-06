# Kim - Attack Path Prioritization

Checklist para priorizacao de caminhos de ataque conforme metodologia ofensiva.

## Mapeamento de Caminhos
- [ ] Todos os entry points identificados durante recon catalogados
- [ ] Attack graph criado com nos (hosts) e edges (paths)
- [ ] Cada path documentado com prerequisites necessarios
- [ ] Dependencies entre paths mapeadas (path A habilita path B)
- [ ] Estimated difficulty atribuida a cada path (Low, Medium, High)
- [ ] Estimated impact atribuido a cada path (Low, Medium, High, Critical)

## Criterios de Priorizacao
- [ ] Paths priorizados por ratio impacto/dificuldade
- [ ] Quick wins identificados (alta probabilidade, baixo esforco)
- [ ] Paths que levam a domain admin mapeados como prioridade
- [ ] Paths que acessam dados sensiveis destacados
- [ ] Paths com menor risco de deteccao identificados
- [ ] Paths com menor risco de disrupcao de servico priorizados
- [ ] Time constraints do engagement considerados na priorizacao

## Validacao de Paths
- [ ] Cada path tem pelo menos uma tecnica viavel identificada
- [ ] Exploits necessarios verificados quanto a confiabilidade
- [ ] Credenciais ou pre-requisitos necessarios listados
- [ ] Fallback paths definidos caso primary path falhe
- [ ] Lateral movement opportunities validadas
- [ ] Privilege escalation vectors mapeados por host

## Documentacao
- [ ] Attack tree visual criado para apresentacao
- [ ] Cada path com referencia a MITRE ATT&CK techniques
- [ ] Risk assessment por path documentado
- [ ] Priorizacao revisada com team lead antes da execucao
- [ ] Decision log mantido durante execucao (path taken, why)
- [ ] Paths nao explorados documentados com justificativa

## Review e Ajuste
- [ ] Priorizacao revisada apos cada phase do engagement
- [ ] Novos paths descobertos durante exploitation incorporados
- [ ] Paths bloqueados ou sem sucesso reclassificados
- [ ] Lesson learned sobre priorizacao documentadas
- [ ] Coverage de paths explorados vs total registrado
