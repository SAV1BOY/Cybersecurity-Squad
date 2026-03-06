# Kim - Proof and Reporting

Checklist para comprovacao de findings e qualidade de report.

## Captura de Provas
- [ ] Screenshot com timestamp para cada finding
- [ ] Command output capturado em formato texto (copiar/colar)
- [ ] Request/response HTTP capturados via proxy (Burp, mitmproxy)
- [ ] Video recording para exploits complexos ou multi-step
- [ ] Hashes de arquivos de evidencia calculados (SHA-256)
- [ ] Evidencias organizadas por finding em diretorio estruturado

## Proof of Concept
- [ ] PoC reproduzivel criado para cada critical/high finding
- [ ] PoC testado para confirmar reproducibilidade
- [ ] PoC documentado com steps claros e numerados
- [ ] PoC contém prerequisites e environmental conditions
- [ ] PoC scripts/payloads salvos e comentados
- [ ] PoC nao causa dano permanente ao target

## Qualidade do Report
- [ ] Executive summary escrito para audiencia C-level
- [ ] Methodology descrita com ferramentas utilizadas
- [ ] Cada finding com titulo descritivo e severity rating
- [ ] Business impact descrito em termos de negocio (nao apenas tecnico)
- [ ] Remediation recommendations especificas e actionable
- [ ] References incluidas (CVE, CWE, OWASP, MITRE ATT&CK)
- [ ] CVSS score calculado e justificado para cada finding

## Narrativa e Storytelling
- [ ] Attack narrative construida end-to-end (initial access to objective)
- [ ] Kill chain documentada para cada path explorado
- [ ] Impact demonstrado com exemplos concretos (dados acessados, sistemas comprometidos)
- [ ] Risk scenarios descritos em termos de ameacas reais
- [ ] Metricas incluidas (tempo para compromise, % de hosts vulneraveis)

## Review e Entrega
- [ ] Report revisado por peer com expertise tecnica
- [ ] Gramatica e formatacao revisadas
- [ ] Sensitive data redacted apropriadamente
- [ ] Report entregue em formato seguro (encrypted PDF)
- [ ] Walkthrough session agendada com cliente
- [ ] Raw data e evidencias arquivadas conforme retention policy
- [ ] Feedback do cliente coletado apos entrega
