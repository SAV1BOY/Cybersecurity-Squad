# Red Team - Safe Testing Rules

Checklist de regras de seguranca para testes de red team.

## Regras Gerais de Seguranca
- [ ] Nenhuma acao sem autorizacao escrita valida
- [ ] Scope boundaries verificados antes de cada acao
- [ ] Production systems tratados com extremo cuidado
- [ ] Backup de configuracoes antes de modificacoes
- [ ] Impacto avaliado antes de cada exploitation attempt
- [ ] Emergency contact list acessivel a todo momento
- [ ] Stop-work authority entendida e respeitada

## Controle de Exploits
- [ ] Apenas exploits testados em lab utilizados em producao
- [ ] DoS exploits proibidos (a menos que explicitamente autorizados)
- [ ] Kernel exploits usados com extrema cautela (crash risk)
- [ ] Memory corruption exploits testados extensivamente antes
- [ ] Exploit stability confirmada (90%+ success rate em lab)
- [ ] Fallback/rollback plan para cada exploit utilizado
- [ ] Anti-crash measures implementadas onde possivel

## Controle de Payloads e Implants
- [ ] Payloads com kill switch ou auto-destruct timer
- [ ] Nenhum payload auto-propagante (worm behavior proibido)
- [ ] Implants nao sobrevivem reboot (a menos que autorizado)
- [ ] C2 callbacks limitados a infraestrutura controlada
- [ ] Encryption em toda comunicacao C2
- [ ] Payload cleanup procedure definida e testada
- [ ] Nenhum implant em sistemas de safety/life-critical

## Protecao de Dados
- [ ] PII e sensitive data nao exfiltrados para fora do ambiente
- [ ] Credenciais capturadas armazenadas encrypted
- [ ] Dados de producao nao copiados para laptops de teste
- [ ] Screenshots limitados ao necessario para evidencia
- [ ] Database dumps proibidos (apenas proof of access)
- [ ] Healthcare, financial, e legal data tratados com cuidado extra

## Incident Response (Red Team Side)
- [ ] Processo definido caso red team cause service disruption
- [ ] Notificacao imediata ao trusted agent em caso de impacto
- [ ] Capacidade de reverter acoes rapidamente
- [ ] Log de todas as acoes mantido para deconfliction
- [ ] Processo para ser "caught" pelo blue team sem comprometer engagement

## Cleanup Obrigatorio
- [ ] Todas as backdoors removidas ao final do engagement
- [ ] Todos os implants desativados e removidos
- [ ] Contas criadas durante teste deletadas
- [ ] Firewall rules ou config changes revertidos
- [ ] Files deployados durante teste removidos
- [ ] Scheduled tasks/cron jobs removidos
- [ ] Registry modifications revertidas (Windows)
- [ ] Cleanup evidence documentada e entregue ao cliente
