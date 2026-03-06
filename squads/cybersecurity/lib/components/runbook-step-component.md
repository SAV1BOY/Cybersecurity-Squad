# Runbook Step Component

Componente para criacao de passos padronizados em runbooks de seguranca.

## Estrutura de um Passo

```
### Step [N]: [Action Title]

**Responsavel**: [Role ou pessoa]
**Tempo estimado**: [X minutos]
**Criticidade**: [Must do | Should do | Nice to have]

#### Acao
[Descricao clara do que fazer]

#### Comando/Procedimento
[Comando exato ou procedimento detalhado]

#### Resultado Esperado
[O que o operador deve observar se executado corretamente]

#### Se Falhar
[Acao alternativa ou escalacao]

#### Evidencia
[O que documentar/salvar como evidencia da execucao]
```

## Exemplo

```
### Step 3: Isolar Host Comprometido

**Responsavel**: SOC Analyst L2+
**Tempo estimado**: 5 minutos
**Criticidade**: Must do

#### Acao
Isolar o host comprometido da rede via EDR console.

#### Comando
1. Acessar CrowdStrike Falcon console
2. Buscar host por hostname ou IP
3. Selecionar "Contain Host"
4. Confirmar isolamento

#### Resultado Esperado
Host em status "Contained" - acesso apenas via EDR.

#### Se Falhar
Contatar infra-team para isolamento via switch port shutdown.
Escalar para IR Lead se isolamento nao for possivel em 10 min.

#### Evidencia
Screenshot do status de containment com timestamp.
```

## Principios

- Cada passo deve ser executavel por alguem que nunca o fez antes
- Incluir comandos exatos, nao instrucoes vagas
- Definir claramente o que fazer quando algo da errado
- Manter passos atomicos - uma acao por step
- Revisar runbooks trimestralmente e apos cada uso real
