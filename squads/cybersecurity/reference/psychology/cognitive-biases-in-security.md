# Vieses Cognitivos em Seguranca

## Visao Geral
Vieses cognitivos afetam tanto atacantes quanto defensores. Entender esses vieses
permite ao squad tomar decisoes mais racionais e explorar vieses de adversarios.

## Vieses que Afetam Defensores

### Vies de Confirmacao
- **O que e**: buscar informacoes que confirmam crencas pre-existentes
- **Em security**: ignorar alertas que contradizem hipotese atual
- **Mitigacao**: devil's advocate em investigacoes, checklists

### Vies de Disponibilidade
- **O que e**: superestimar probabilidade de eventos facilmente lembrados
- **Em security**: focar em ransomware por estar na midia, ignorar insider threat
- **Mitigacao**: usar threat intelligence baseada em dados, nao em manchetes

### Efeito Dunning-Kruger
- **O que e**: incompetentes superestimam habilidades, experts subestimam
- **Em security**: juniores podem ser excessivamente confiantes em defesas
- **Mitigacao**: promover humildade tecnica, red team exercises regulares

### Vies de Normalidade
- **O que e**: assumir que coisas continuarao funcionando normalmente
- **Em security**: "isso nunca aconteceu, entao nao vai acontecer"
- **Mitigacao**: simulacoes regulares, pre-mortem analysis

### Ancoragem
- **O que e**: depender demais da primeira informacao recebida
- **Em security**: primeiro alerta define toda a investigacao
- **Mitigacao**: considerar multiplas hipoteses em paralelo

### Fadiga de Alerta
- **O que e**: dessensibilizacao por excesso de alertas
- **Em security**: ignorar alertas reais em mar de false positives
- **Mitigacao**: tuning rigoroso de regras, priorizacao automatizada

## Vieses que Afetam Atacantes

### Overconfidence
- Atacantes que subestimam defesas
- Oportunidade: honeypots que exploram excesso de confianca

### Sunk Cost Fallacy
- Persistir em ataque ineficaz por investimento ja feito
- Oportunidade: deteccao de persistencia e re-tentativas

### Tunnel Vision
- Focar em um vetor e ignorar defesas em outros
- Oportunidade: defesa em profundidade funciona

## Vieses em Decisoes de Risco

### Otimismo Irreal
- Subestimar probabilidade de eventos negativos
- Impacto: investimento insuficiente em seguranca
- Comunicacao: usar dados concretos, nao estimativas abstratas

### Aversao a Perda
- Medo de perda e mais forte que desejo de ganho
- Uso positivo: framing de riscos como potenciais perdas
- Comunicacao: "voce pode perder X" > "voce pode ganhar Y em protecao"

## Aplicacao no Squad
- **Decisoes de IR**: usar checklists para contornar vieses
- **Risk Communication**: framing de riscos considerando vieses do audience
- **Threat Hunting**: considerar hipoteses alternativas
- **Training**: ensinar reconhecimento de vieses proprios
- **Red Team**: explorar vieses dos defensores nas operacoes

## Notas do Squad
Autoconsciencia sobre vieses e a melhor defesa. Promover cultura onde
questionar decisoes e bem-vindo, nao visto como insubordinacao.
