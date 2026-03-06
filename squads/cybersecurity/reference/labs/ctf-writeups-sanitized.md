# CTF Writeups - Guia e Templates Sanitizados

## Objetivo
Documentar metodologias e aprendizados de Capture The Flag competitions de
forma sanitizada, sem expor flags ou solucoes diretas de competicoes ativas.

## Categorias de CTF

### Web Exploitation
- SQL Injection (blind, union-based, time-based)
- Cross-Site Scripting (reflected, stored, DOM)
- Server-Side Request Forgery (SSRF)
- Server-Side Template Injection (SSTI)
- Insecure Deserialization
- Business logic flaws
- Authentication bypasses

### Binary Exploitation (Pwn)
- Buffer overflow (stack e heap)
- Return-Oriented Programming (ROP)
- Format string vulnerabilities
- Use-after-free
- Race conditions
- Shellcode development

### Reverse Engineering
- Static analysis com Ghidra/IDA
- Dynamic analysis com GDB/x64dbg
- Malware analysis basico
- Android APK reversing
- .NET/Java decompilation

### Cryptography
- Classic ciphers (Caesar, Vigenere, XOR)
- RSA attacks (small e, common modulus)
- AES mode attacks (ECB, CBC padding oracle)
- Hash collision e length extension
- PRNG prediction

### Forensics
- Disk image analysis
- Memory forensics com Volatility
- Network packet analysis
- Steganography detection
- Log analysis e timeline creation

## Template de Writeup

### Cabecalho
- Nome do desafio e categoria
- Dificuldade estimada
- Ferramentas utilizadas
- Tecnicas aplicadas (mapeadas para ATT&CK quando possivel)

### Corpo
1. **Reconnaissance**: o que foi descoberto inicialmente
2. **Analysis**: analise do problema e hipoteses
3. **Exploitation**: passo a passo da solucao
4. **Lessons Learned**: o que foi aprendido
5. **Real-World Application**: como se aplica ao trabalho do squad

## CTFs Recomendados
- HackTheBox (machines e challenges)
- TryHackMe (learning paths)
- PicoCTF (iniciantes)
- OverTheWire (wargames progressivos)
- CTFtime.org (competicoes ao vivo)

## Praticas do Squad
- Participar de pelo menos 1 CTF por trimestre como equipe
- Rodar internal CTFs para treinamento
- Documentar todos os writeups no repositorio interno
- Sessoes de knowledge sharing apos competicoes

## Notas do Squad
CTFs sao a melhor forma de manter habilidades afiadas. Incentivar participacao
de todos os membros, independente de nivel de experiencia.
