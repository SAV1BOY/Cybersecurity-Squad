# Mobile Assessment Quality Gate

Checklist de qualidade para avaliacao de seguranca de aplicacoes mobile.

## Preparacao do Ambiente
- [ ] Dispositivo de teste (rooted/jailbroken) configurado
- [ ] Proxy de interceptacao (Burp/mitmproxy) configurado com cert trust
- [ ] Frida/Objection instalados e funcionais
- [ ] APK/IPA obtido e backup realizado
- [ ] OWASP MASTG utilizado como referencia de teste

## Static Analysis
- [ ] Decompilation realizada com sucesso (jadx, Hopper, Ghidra)
- [ ] Hardcoded secrets buscados (API keys, credentials, tokens)
- [ ] Insecure storage identificado (SharedPreferences, Keychain misuse)
- [ ] Certificate pinning implementation revisada
- [ ] Code obfuscation avaliada
- [ ] Third-party SDKs e libraries catalogados e auditados
- [ ] AndroidManifest.xml / Info.plist analisados para permissions excessivas

## Dynamic Analysis
- [ ] Network traffic interceptado e analisado
- [ ] SSL/TLS pinning bypass testado
- [ ] Authentication flow testado (token storage, session handling)
- [ ] Local data storage auditado (SQLite, files, logs)
- [ ] IPC mechanisms testados (intents, deep links, URL schemes)
- [ ] Clipboard data leakage verificado
- [ ] Screenshot/screen recording protection verificado
- [ ] Biometric authentication bypass testado

## Platform-Specific (Android)
- [ ] Exported components testados (activities, services, receivers)
- [ ] Content providers auditados para data leakage
- [ ] WebView security verificada (JavaScript interface, file access)
- [ ] Backup flag verificado (android:allowBackup)
- [ ] Root detection bypass testado

## Platform-Specific (iOS)
- [ ] Keychain usage auditada (protection classes)
- [ ] ATS (App Transport Security) configuration verificada
- [ ] Jailbreak detection bypass testado
- [ ] Binary protections verificadas (PIE, ARC, stack canaries)

## Evidencias e Entrega
- [ ] OWASP MASVS coverage documentada
- [ ] PoC para cada finding com steps to reproduce
- [ ] Remediation recommendations especificas para mobile
- [ ] Report revisado por peer antes da entrega
