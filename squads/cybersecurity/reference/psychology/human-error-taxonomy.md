# Taxonomia de Erro Humano em Seguranca

## Visao Geral
Classificar erros humanos em seguranca permite ao squad entender padroes,
projetar controles mais eficazes e reduzir a frequencia e impacto de
falhas humanas.

## Classificacao de Erros (Reason)

### Slips (Deslizes)
- **Definicao**: acao incorreta executada automaticamente
- **Exemplo**: clicar em "Reply All" com informacao sensivel
- **Exemplo**: digitar senha no campo de username
- **Causa**: falta de atencao em tarefas rotineiras
- **Mitigacao**: confirmacao antes de acoes criticas, undo

### Lapses (Lapsos)
- **Definicao**: falha de memoria ou omissao
- **Exemplo**: esquecer de revogar acesso de ex-funcionario
- **Exemplo**: nao aplicar patch critico por esquecimento
- **Causa**: sobrecarga cognitiva, falta de checklists
- **Mitigacao**: automacao, checklists, lembretes

### Mistakes (Erros de Julgamento)
- **Definicao**: acao errada baseada em raciocinio incorreto
- **Exemplo**: classificar alerta real como false positive
- **Exemplo**: escolher algoritmo de criptografia inadequado
- **Causa**: conhecimento insuficiente, vieses cognitivos
- **Mitigacao**: treinamento, peer review, guidelines

### Violations (Violacoes)
- **Definicao**: desvio deliberado de procedimento
- **Exemplo**: desabilitar firewall para "testar rapidamente"
- **Exemplo**: compartilhar senha de servico para conveniencia
- **Causa**: procedimentos percebidos como ineficientes
- **Mitigacao**: entender porque pessoas violam, redesenhar processos

## Aplicacao em Seguranca

### Erros em Desenvolvimento
- **Slip**: commit de credencial em repositorio publico
- **Lapse**: esquecer de validar input em endpoint novo
- **Mistake**: implementar criptografia custom
- **Violation**: desabilitar SAST para acelerar pipeline

### Erros em Operacoes
- **Slip**: aplicar patch no servidor errado
- **Lapse**: esquecer de renovar certificado TLS
- **Mistake**: configurar security group muito permissivo
- **Violation**: usar conta root para tarefas rotineiras

### Erros em Resposta a Incidentes
- **Slip**: enviar IOC para canal publico ao inves de privado
- **Lapse**: esquecer de preservar evidencia volatil
- **Mistake**: conter sistema errado
- **Violation**: pular etapas do playbook por pressao

## Modelo do Queijo Suico (Swiss Cheese Model)
- Cada camada de defesa tem "furos" (imperfeicoes)
- Incidentes ocorrem quando furos se alinham entre camadas
- Adicionar camadas reduz probabilidade de alinhamento
- Nenhuma camada unica e perfeita

## Estrategias de Reducao de Erro

### Design Out
- Eliminar oportunidade de erro (automacao)
- Tornar impossivel a acao insegura
- Exemplo: secrets management automatizado

### Guard Against
- Detectar erro antes que cause dano
- Confirmacoes, validacoes, checks
- Exemplo: PR review obrigatorio para infra changes

### Make Reversible
- Permitir reverter acoes erradas
- Undo, rollback, versioning
- Exemplo: infrastructure as code com rollback

### Make Visible
- Tornar erros facilmente detectaveis
- Monitoring, alerting, dashboards
- Exemplo: alertas de compliance deviation

## Metricas
- Frequencia de erros por tipo e categoria
- Tempo de deteccao de erros
- Impacto de erros por tipo
- Eficacia de controles preventivos

## Notas do Squad
Erros humanos sao inevitaveis. O objetivo nao e eliminar erros, mas
projetar sistemas que tolerem erros e minimizem suas consequencias.
