# Create Engagement Folder

Script para criar a estrutura padronizada de pastas para um novo engagement de seguranca.

## Descricao

Gera toda a arvore de diretorios necessaria para organizar artefatos de um engagement, incluindo arquivos iniciais de tracking e metadata.

## Inputs

- `engagement_id` - Identificador unico (ex: ENG-2026-015)
- `engagement_type` - Tipo (pentest, review, audit, hunting, incident)
- `client_or_system` - Nome do cliente ou sistema
- `lead` - Nome do engagement lead

## Logica

1. Validar formato do engagement_id (ENG-YYYY-NNN)
2. Verificar que o engagement_id nao existe no repositorio
3. Criar diretorio raiz: `[engagement_id]-[client_or_system]/`
4. Criar subpastas padrao:
   - `evidence/` - Evidencias coletadas durante o engagement
   - `reports/` - Relatorios draft e final
   - `notes/` - Anotacoes e rascunhos da equipe
   - `tools/` - Scripts e ferramentas customizadas
   - `comms/` - Comunicacoes com stakeholders
5. Gerar arquivo `metadata.yaml` com informacoes do engagement
6. Gerar arquivo `status.md` com tracking basico
7. Copiar checklists relevantes para o tipo de engagement

## Estrutura Gerada

```
ENG-2026-015-portal-cliente/
  evidence/
  reports/
  notes/
  tools/
  comms/
  metadata.yaml
  status.md
  checklist-pre-engagement.md
  checklist-closeout.md
```

## Conteudo do metadata.yaml

```yaml
engagement_id: ENG-2026-015
type: pentest
target: portal-cliente
lead: "Analyst Name"
created: 2026-03-06
status: active
```

## Output

- Estrutura de pastas criada no repositorio de engagements
- Arquivos de metadata e tracking inicializados
- Confirmacao de criacao com caminho completo

## Validacoes

- Rejeitar IDs duplicados
- Rejeitar tipos de engagement nao reconhecidos
- Verificar permissoes de escrita no diretorio destino
