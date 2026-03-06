# The Art of Software Security Assessment - Ficha de Referencia

## Metadados
- **Titulo**: The Art of Software Security Assessment: Identifying and Preventing Software Vulnerabilities
- **Autor**: Mark Dowd, John McDonald, Justin Schuh
- **Categoria**: Software Security / Code Auditing

## Descricao Geral
O guia mais completo para auditoria de seguranca de software. Cobre tecnicas
de analise de codigo em C, C++, Java e linguagens web, com foco em encontrar
vulnerabilidades complexas que ferramentas automatizadas perdem.

## Conceitos-Chave
- Code auditing methodology e strategies
- Memory corruption (buffer overflows, heap overflows, use-after-free)
- Integer overflow e arithmetic vulnerabilities
- Race conditions e concurrency issues
- Format string vulnerabilities
- C/C++ specific security issues
- Java e managed language security
- Web tier vulnerabilities (injection, XSS)
- Network protocol analysis e fuzzing
- Design review e architectural assessment

## Por Que Importa para o Squad
Code review manual continua sendo essencial para encontrar vulnerabilidades
que scanners automatizados nao detectam. Este livro ensina a pensar como um
auditor de seguranca de codigo.

## Como o Squad Utiliza
- **Code Audit**: metodologia para auditorias de codigo
- **SAST Complement**: complementar resultados de ferramentas automatizadas
- **Training**: formacao de especialistas em code review
- **Vulnerability Research**: base para pesquisa de vulns
- **Consulting**: guia para assessments de software

## Complementa
- mcgraw-software-security.md (processo de software security)
- erickson-hacking-art-of-exploitation.md (exploitation)
- manico-iron-clad-java.md (secure coding)

## Nivel de Profundidade
Avancado - requer forte background em programacao.

## Notas do Squad
Mesmo com a evolucao de ferramentas SAST, a habilidade de leitura manual de
codigo e insubstituivel. Dedicar tempo para praticar auditorias manuais.
