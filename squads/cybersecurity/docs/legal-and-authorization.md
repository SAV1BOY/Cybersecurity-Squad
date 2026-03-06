# Legal and Authorization

Diretrizes legais e de autorizacao para atividades de seguranca ofensiva e defensiva.

## Principio Fundamental

Nenhuma atividade de teste ou avaliacao de seguranca deve ser conduzida sem autorizacao formal e documentada. A ausencia de autorizacao pode configurar crime informatico.

## Autorizacao para Pentest

### Requisitos Obrigatorios
- Authorization letter assinada pelo owner do sistema ou representante legal
- Scope statement detalhando exatamente o que pode ser testado
- Rules of engagement definindo limites, horarios e restricoes
- Contatos de emergencia para comunicacao durante o teste
- Periodo de validade da autorizacao

### O que Deve Constar na Autorizacao
- Identificacao das partes (testador e autorizante)
- Lista de IPs, dominios e sistemas autorizados
- Tecnicas permitidas e proibidas
- Janela de execucao com datas e horarios
- Assinaturas de ambas as partes com data

### Restricoes Comuns
- Nao executar ataques de negacao de servico sem aprovacao explicita
- Nao acessar dados reais de clientes alem do necessario para comprovar impacto
- Nao exfiltrar dados para fora do ambiente controlado
- Nao modificar ou deletar dados em producao

## Autorizacao para Incident Response

- A equipe de IR possui autorizacao permanente para acoes de containment conforme politica organizacional
- Acoes destrutivas (wipe, isolamento) requerem aprovacao do incident commander
- Coleta de evidencias deve seguir procedimentos que preservem admissibilidade legal

## Tratamento de Dados Pessoais

- Toda atividade que envolva dados pessoais deve respeitar a LGPD e regulacoes aplicaveis
- Dados pessoais encontrados durante testes devem ser reportados mas nao coletados desnecessariamente
- Logs e evidencias contendo dados pessoais devem ser protegidos e descartados conforme politica de retencao

## Responsabilidades do Squad

- Manter registro de todas as autorizacoes vigentes e expiradas
- Nunca exceder o escopo autorizado, mesmo que acidentalmente
- Reportar imediatamente qualquer acao fora do escopo
- Preservar confidencialidade de todas as informacoes obtidas

## Descarte de Informacoes

- Credenciais obtidas durante testes devem ser descartadas apos o relatorio
- Evidencias devem ser armazenadas conforme politica de retencao e depois destruidas
- Ferramentas e payloads customizados nao devem ser compartilhados externamente

## Em Caso de Duvida

- Consulte o departamento juridico antes de prosseguir
- Na duvida sobre escopo, pare e valide com o autorizante
- Documente todas as decisoes e justificativas
- Nunca assuma que algo esta autorizado sem confirmacao explicita
