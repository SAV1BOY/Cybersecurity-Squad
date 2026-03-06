# Weidman - Payload Safety Audit

Checklist de seguranca para auditoria de payloads utilizados em testes.

## Design do Payload
- [ ] Payload objetivo claramente definido (reverse shell, info gathering)
- [ ] Payload funcionalidade limitada ao minimo necessario
- [ ] Nenhuma funcionalidade destrutiva incluida (wiper, ransomware-like)
- [ ] Payload nao se auto-propaga (no worm behavior)
- [ ] Kill switch ou timeout incorporado no payload
- [ ] Payload nao persiste apos reboot (a menos que autorizado)
- [ ] Callback destination controlado pelo tester (C2 proprio)

## Teste em Lab
- [ ] Payload testado em lab isolado antes de uso em producao
- [ ] Comportamento do payload monitorado e documentado
- [ ] Resource consumption avaliado (CPU, RAM, disk, network)
- [ ] Stability do payload verificada sob diferentes condicoes
- [ ] Cleanup mechanism testado e funcional
- [ ] AV/EDR detection rate verificado (para planning, nao evasion)
- [ ] Payload nao causa crash ou DoS no target service

## Seguranca do C2
- [ ] C2 server hardened e sob controle exclusivo do tester
- [ ] Comunicacao C2 encrypted (HTTPS, DNS over HTTPS)
- [ ] C2 credentials unicas para cada engagement
- [ ] C2 logs habilitados para auditoria
- [ ] C2 infrastructure isolada por engagement
- [ ] Domain/IP do C2 nao reutilizado entre clientes
- [ ] C2 descomissionado apos encerramento do engagement

## Controle de Acesso ao Payload
- [ ] Payload armazenado encrypted quando nao em uso
- [ ] Acesso ao payload restrito a membros autorizados do time
- [ ] Payload source code em repositorio com access control
- [ ] Payloads custom nao compartilhados publicamente
- [ ] Versioning aplicado para cada variante de payload
- [ ] Inventory de payloads deployados mantido atualizado

## Cleanup e Destruicao
- [ ] Todos os payloads removidos dos targets apos teste
- [ ] Processos de payload terminados em todos os hosts
- [ ] Artefatos de payload removidos (files, registry, services)
- [ ] C2 callbacks confirmados como cessados
- [ ] Payload binaries deletados de staging servers
- [ ] Confirmacao de cleanup documentada e assinada

## Documentacao
- [ ] Cada payload utilizado documentado (hash, filename, config)
- [ ] Deploy time e remove time registrados por host
- [ ] Comportamento observado documentado
- [ ] Incidentes de safety (se ocorreram) documentados
- [ ] Report de payload audit entregue ao time lead
