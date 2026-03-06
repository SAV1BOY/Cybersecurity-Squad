# Threat Model Component

Componente para documentacao padronizada de threat models usando STRIDE.

## Estrutura

```
## Threat Model: [System/Feature Name]

### System Description
[Descricao do sistema, seus componentes e fluxo de dados]

### Data Flow Diagram
[Referencia ao DFD ou descricao textual dos fluxos]

### Trust Boundaries
[Fronteiras de confianca identificadas]

### Assets
[Ativos valiosos que requerem protecao]

### Threat Actors
[Perfil dos adversarios relevantes]

### STRIDE Analysis
[Ameacas identificadas por categoria]

### Mitigations
[Controles propostos para cada ameaca]

### Risk Assessment
[Avaliacao de risco residual]
```

## STRIDE Categories

| Category | Descricao | Propriedade Violada |
|----------|-----------|-------------------|
| Spoofing | Personificacao de identidade | Authentication |
| Tampering | Modificacao nao autorizada de dados | Integrity |
| Repudiation | Negacao de acoes realizadas | Non-repudiation |
| Information Disclosure | Exposicao de dados sensiveis | Confidentiality |
| Denial of Service | Interrupcao de disponibilidade | Availability |
| Elevation of Privilege | Obtencao de permissoes indevidas | Authorization |

## Template de Ameaca

```
### THREAT-001: [Titulo]
- **STRIDE**: [Categoria]
- **Componente**: [Parte do sistema afetada]
- **Descricao**: [Como o ataque seria realizado]
- **Likelihood**: [High | Medium | Low]
- **Impact**: [High | Medium | Low]
- **Mitigation**: [Controle proposto]
- **Status**: [Mitigated | Accepted | Open]
```

## Quando Aplicar

- Novos sistemas ou features significativas
- Mudancas arquiteturais em sistemas existentes
- Integracao com novos terceiros ou APIs
- Apos incidentes que revelam gaps no modelo existente
