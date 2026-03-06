# Evidence Chain Quality Gate

Checklist de qualidade para cadeia de evidencias.

## Coleta de Evidencias
- [ ] Cada finding possui pelo menos uma evidencia associada
- [ ] Screenshots capturados com timestamp visivel
- [ ] Request/Response capturados em formato raw
- [ ] Command output preservado com comando executado
- [ ] Tool output exportado em formato nativo e legivel
- [ ] Video recording para exploracao de findings complexos

## Integridade
- [ ] Hash (SHA-256) calculado para cada arquivo de evidencia
- [ ] Chain of custody documentada (quem coletou, quando, onde)
- [ ] Evidencias armazenadas em repositorio com controle de acesso
- [ ] Nenhuma evidencia editada sem documentar a alteracao
- [ ] Timestamps sincronizados entre fontes de evidencia
- [ ] Backup das evidencias realizado em local separado

## Organizacao
- [ ] Naming convention consistente para arquivos de evidencia
- [ ] Diretorio structure organizado por finding ou por fase
- [ ] Index file mapeando evidencias a findings
- [ ] Metadata registrada (tool, date, tester, target)
- [ ] Evidencias cross-referenced no report final
- [ ] Formato de arquivo acessivel sem software proprietario

## Reproducibilidade
- [ ] Steps to reproduce documentados com cada evidencia
- [ ] Payloads e scripts utilizados preservados
- [ ] Ambiente de teste documentado (IPs, versoes, configs)
- [ ] Sequencia de comandos reproduzivel por terceiro
- [ ] Custom tools ou scripts versionados e comentados

## Redaction e Protecao
- [ ] PII e dados sensiveis redacted em evidencias publicas
- [ ] Credenciais obtidas durante teste protegidas/encrypted
- [ ] Client proprietary data tratada conforme NDA
- [ ] Evidencias classificadas conforme sensitivity level
- [ ] Prazo de retencao e destruction policy definidos

## Validacao
- [ ] Peer reviewer verificou completude da evidencia
- [ ] Cada finding no report tem evidencia correspondente
- [ ] Nenhum gap na timeline de atividades
- [ ] Evidencias suportam a severity rating atribuida
- [ ] Cadeia de evidencia pronta para auditoria externa
