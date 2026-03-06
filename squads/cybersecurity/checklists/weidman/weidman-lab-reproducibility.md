# Weidman - Lab Reproducibility

Checklist para garantir reproducibilidade de testes em laboratorio.

## Configuracao do Lab
- [ ] Lab environment documentado (VMs, network config, snapshots)
- [ ] Target systems replicam ambiente do cliente (OS, services, versions)
- [ ] Network topology do lab mapeada e documentada
- [ ] Snapshots criados antes de cada fase de teste
- [ ] Isolation do lab garantida (sem acesso a producao)
- [ ] Internet connectivity controlada e documentada
- [ ] DNS e DHCP configurados conforme ambiente real

## Ferramentas e Versoes
- [ ] Toolset utilizado documentado com versoes exatas
- [ ] Custom scripts versionados em repositorio (Git)
- [ ] Exploit frameworks com versao registrada (Metasploit, Cobalt Strike)
- [ ] Wordlists e payload lists documentadas
- [ ] Configuration files de tools salvos para reproducao
- [ ] VM images/snapshots versionados e acessiveis

## Documentacao de Testes
- [ ] Cada teste documentado com pre-conditions completas
- [ ] Comando exato utilizado registrado (copy/paste ready)
- [ ] Parametros e flags documentados com explicacao
- [ ] Expected output vs actual output registrado
- [ ] Environment variables necessarias documentadas
- [ ] Ordem de execucao dos steps documentada quando relevante
- [ ] Timing dependencies anotadas (se aplicavel)

## Validacao de Reproducibilidade
- [ ] Cada PoC reproduzido pelo menos uma vez em lab
- [ ] Segundo tester reproduziu findings criticos independentemente
- [ ] Lab re-deployment testado a partir da documentacao
- [ ] Automated scripts reproduzem resultados consistentemente
- [ ] Edge cases e failure modes documentados
- [ ] Timeout e retry logic documentados para testes flaky

## Compartilhamento e Handoff
- [ ] Lab setup guide criado para novos membros do time
- [ ] Dependencies e prerequisites listados claramente
- [ ] Troubleshooting guide para problemas comuns
- [ ] Lab artifacts (scripts, configs, wordlists) compartilhados
- [ ] Knowledge transfer session realizada com equipe
- [ ] Lab environment disponivel para retest futuro

## Manutencao
- [ ] Lab atualizado quando novas versoes de targets sao relevantes
- [ ] Snapshots antigos limpos periodicamente
- [ ] Storage adequado para lab artifacts garantido
- [ ] Lab access controls revisados periodicamente
