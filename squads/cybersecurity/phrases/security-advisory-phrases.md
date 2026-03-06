# Security Advisory Phrases

Frases padronizadas para redigir advisories de seguranca internas e externas.

## Cabecalho e Classificacao

- "Security Advisory [ID] - Severidade: [Critical/High/Medium/Low] - Publicado em [data]."
- "Este advisory descreve uma vulnerabilidade identificada em [produto/sistema] que requer atencao imediata."
- "Classificacao de impacto: [Confidentiality/Integrity/Availability] - Sistemas afetados: [lista]."

## Descricao da Vulnerabilidade

- "Foi identificada uma vulnerabilidade de [tipo] que permite a um atacante [acao] em sistemas afetados."
- "A falha reside no componente [nome] e pode ser explorada remotamente sem necessidade de autenticacao."
- "A vulnerabilidade afeta as versoes [lista de versoes] do [produto] e esta registrada como [CVE-ID]."
- "Exploits publicos estao disponiveis para esta vulnerabilidade, aumentando significativamente o risco de exploracao."

## Impacto

- "A exploracao bem-sucedida permite [execucao de codigo remoto / escalacao de privilegios / acesso a dados]."
- "Sistemas expostos a internet sao especialmente vulneraveis e devem ser priorizados na remediacao."
- "O impacto potencial inclui comprometimento total do sistema afetado e possivel movimentacao lateral no ambiente."

## Mitigacao e Remediacao

- "O vendor disponibilizou patch de seguranca na versao [numero]. Recomendamos atualizacao imediata."
- "Caso a atualizacao nao seja possivel imediatamente, as seguintes mitigacoes temporarias podem ser aplicadas: [lista]."
- "Recomendamos verificar se os sistemas afetados em seu ambiente estao na lista de versoes vulneraveis."
- "Apos aplicar o patch, verifique os logs do sistema para sinais de exploracao anterior."

## Deteccao

- "Indicadores de comprometimento (IOCs) associados a exploracao desta vulnerabilidade: [lista]."
- "Detection rules foram atualizadas no SIEM para identificar tentativas de exploracao."
- "Recomendamos executar os seguintes comandos para verificar se o sistema foi comprometido: [instrucoes]."

## Timeline e Atualizacoes

- "Este advisory sera atualizado conforme novas informacoes estejam disponiveis."
- "Proxima revisao programada para [data]. Caso a situacao mude, uma atualizacao sera emitida antes."
- "Historico de atualizacoes: [data] - Publicacao inicial. [data] - Adicionados IOCs."

## Contato

- "Para duvidas sobre este advisory, entre em contato com a equipe de seguranca via [canal]."
- "Reporte exploracoes suspeitas imediatamente atraves do canal de incidentes [contato]."
