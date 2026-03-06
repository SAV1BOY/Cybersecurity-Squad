# Psicologia do Atacante

## Visao Geral
Entender como atacantes pensam, decidem e operam permite ao squad antecipar
movimentos, melhorar deteccao e criar defesas mais eficazes.

## Perfis de Atacantes

### Script Kiddie
- **Motivacao**: curiosidade, status entre pares, diversao
- **Habilidade**: baixa, usa ferramentas prontas
- **Persistencia**: baixa, desiste facilmente
- **Defesa**: controles basicos bloqueiam maioria dos ataques

### Hacktivista
- **Motivacao**: ideologia, ativismo, exposicao de injusticas
- **Habilidade**: variavel, de basica a avancada
- **Persistencia**: alta quando motivado pela causa
- **Defesa**: reputacao e posicionamento publico influenciam targeting

### Cybercriminoso Organizado
- **Motivacao**: lucro financeiro
- **Habilidade**: alta, acesso a ferramentas sofisticadas
- **Persistencia**: alta enquanto lucrativo (ROI-driven)
- **Defesa**: aumentar custo de ataque, reduzir ROI

### Nation-State APT
- **Motivacao**: espionagem, sabotagem, influencia geopolitica
- **Habilidade**: extremamente alta, zero-days, custom tools
- **Persistencia**: muito alta, operacoes de meses/anos
- **Defesa**: assume breach, foco em deteccao e contencao

### Insider Malicioso
- **Motivacao**: vinganca, ganho financeiro, ideologia
- **Habilidade**: variavel, mas possui acesso legitimo
- **Persistencia**: variavel, depende da motivacao
- **Defesa**: monitoramento comportamental, least privilege

## Processos Cognitivos do Atacante

### Avaliacao de Alvo (Target Selection)
- Atacantes buscam alvos com maior retorno e menor risco
- Analise de custo-beneficio: dificuldade vs recompensa
- Oportunismo: muitos ataques nao sao direcionados
- Defesa: parecer um alvo dificil (deterrence)

### Tomada de Decisao durante Ataque
- Path of least resistance (caminho de menor resistencia)
- Exploracao de surpresa e velocidade
- Adaptacao rapida quando bloqueado
- Uso de ferramentas familiares quando possivel

### Persistencia vs Abandono
- Avaliacao continua de risco de deteccao
- Sunk cost pode motivar persistencia irracional
- Detectar e comunicar deteccao pode deter atacante
- "Making noise" como tatica de deterrence

## Principios para o Squad

### Think Like an Attacker
- Em threat modeling, pensar "o que eu faria?"
- Attack trees para mapear caminhos possiveis
- Assume breach: atacante ja pode estar dentro
- Priorizar defesas onde atacantes focam esforcos

### Aumentar Custo de Ataque
- Defense in depth para aumentar tempo e esforco
- Deteccao rapida reduz janela de operacao
- Resposta eficiente minimiza impacto
- Deception (honeypots) aumenta incerteza do atacante

### Explorar Fraquezas do Atacante
- Atacantes tambem cometem erros (OPSEC failures)
- Impaciencia pode levar a erros detectaveis
- Ferramentas conhecidas tem assinaturas conhecidas
- Reutilizacao de infraestrutura facilita atribuicao

## Notas do Squad
Estudar threat intelligence reports sobre TTPs de adversarios relevantes
ao contexto do squad. Entender motivacao do atacante ajuda a priorizar
defesas e prever comportamento.
