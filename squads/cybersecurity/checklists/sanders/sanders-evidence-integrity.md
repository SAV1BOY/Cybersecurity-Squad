# Sanders - Evidence Integrity

Checklist para garantia de integridade de evidencias digitais.

## Coleta Inicial
- [ ] Evidencia identificada e catalogada antes de qualquer manipulacao
- [ ] Ordem de volatilidade respeitada (memoria, processos, disk)
- [ ] Write blocker utilizado para midias fisicas
- [ ] Forensic imaging realizado com ferramenta validada
- [ ] Original evidence preservada sem alteracao
- [ ] Working copy criada para analise
- [ ] Ambiente de coleta documentado (sistema, tools, versoes)

## Hashing e Verificacao
- [ ] Hash SHA-256 calculado para cada item de evidencia no momento da coleta
- [ ] Hash registrado em chain of custody form
- [ ] Hash recalculado apos transferencia para verificar integridade
- [ ] Hash verificado antes de cada sessao de analise
- [ ] Dual hashing aplicado (SHA-256 + MD5) para compatibilidade
- [ ] Hash values armazenados em local separado da evidencia
- [ ] Ferramenta de hashing validada e documentada

## Chain of Custody
- [ ] Formulario de chain of custody iniciado na coleta
- [ ] Cada transferencia de custodia registrada (who, when, why)
- [ ] Evidencias fisicas em storage seguro (locked cabinet/room)
- [ ] Evidencias digitais em storage com access control e audit log
- [ ] Acesso a evidencias restrito a pessoal autorizado
- [ ] Registro de quem acessou cada evidencia e quando
- [ ] Seals/tamper-evident bags utilizados para midias fisicas

## Storage e Preservacao
- [ ] Evidencias armazenadas em ambiente controlado
- [ ] Backup de evidencias digitais realizado em local separado
- [ ] Retention policy definida e seguida
- [ ] Degradacao de midia monitorada (para storage longo)
- [ ] Encryption aplicada em evidencias digitais armazenadas
- [ ] Access logs do storage revisados periodicamente
- [ ] Disaster recovery plan para evidencias definido

## Analise Segura
- [ ] Analise realizada apenas em working copies (nunca no original)
- [ ] Ferramentas forenses validadas e com versoes documentadas
- [ ] Resultados da analise documentados com referencia a evidencia
- [ ] Screenshots e exports da analise preservados separadamente
- [ ] Analise reproduzivel por terceiro com as mesmas tools

## Documentacao e Auditabilidade
- [ ] Log de todas as acoes realizadas sobre evidencias
- [ ] Metodologia de coleta e analise documentada
- [ ] Ferramentas utilizadas listadas com versoes
- [ ] Expert qualifications documentadas (para admissibilidade legal)
- [ ] Report de integridade de evidencias preparado
- [ ] Processo pronto para auditoria externa ou judicial
- [ ] Destruction schedule definido e aprovado
