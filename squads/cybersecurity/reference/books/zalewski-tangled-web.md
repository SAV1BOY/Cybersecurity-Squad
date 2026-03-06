# The Tangled Web - Ficha de Referencia

## Metadados
- **Titulo**: The Tangled Web: A Guide to Securing Modern Web Applications
- **Autor**: Michal Zalewski
- **Categoria**: Web Security / Browser Security

## Descricao Geral
Analise profunda da seguranca de browsers e da stack web. Escrito por um dos
pesquisadores de seguranca mais respeitados do Google, o livro detalha as
complexidades e inconsistencias que geram vulnerabilidades web.

## Conceitos-Chave
- HTTP protocol security implications
- Same-Origin Policy (SOP) e suas limitacoes
- Content-Type handling e MIME sniffing attacks
- Cookie security model e seus problemas
- Cross-origin resource sharing (CORS)
- JavaScript security model
- DOM security e innerHTML risks
- CSS-based attacks e data exfiltration
- Browser plugin security (Flash, Java)
- Content Security Policy (CSP)

## Por Que Importa para o Squad
Entender como browsers funcionam e fundamental para web application security.
Muitas vulnerabilidades surgem de comportamentos inesperados do browser que
este livro documenta meticulosamente.

## Como o Squad Utiliza
- **Web Pentesting**: entender nuances do browser
- **CSP Design**: configuracao de Content Security Policy
- **AppSec Reviews**: avaliar riscos de client-side code
- **Training**: aprofundamento em browser security
- **Bypass Research**: encontrar formas de bypass de controles

## Complementa
- stuttard-web-application-hackers.md (web app attacks)
- manico-iron-clad-java.md (defesa server-side)
- dowd-art-of-software-security.md (analise de seguranca)

## Nivel de Profundidade
Avancado - requer bom entendimento de HTTP e JavaScript.

## Notas do Squad
Apesar de alguns topicos (Flash, Java plugins) estarem obsoletos, os
fundamentos de browser security permanecem criticos e relevantes.
