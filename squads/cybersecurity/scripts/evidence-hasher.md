# Evidence Hasher

Script para gerar e verificar hashes de integridade de evidencias de seguranca.

## Descricao

Calcula hashes criptograficos para evidencias coletadas durante engagements e incidentes, garantindo integridade e chain of custody para possivel uso juridico.

## Inputs

- `evidence_path` - Caminho para arquivo ou diretorio de evidencias
- `algorithm` - Algoritmo de hash (sha256, sha512; padrao: sha256)
- `mode` - Modo de operacao (generate, verify)
- `manifest_path` - Caminho para o arquivo de manifesto (para verificacao)

## Logica - Modo Generate

1. Listar todos os arquivos no caminho especificado (recursivo se diretorio)
2. Para cada arquivo:
   - Calcular hash com o algoritmo selecionado
   - Registrar: nome do arquivo, tamanho, hash, timestamp de calculo
3. Gerar manifesto com todos os hashes
4. Calcular hash do proprio manifesto para tamper detection
5. Exibir resumo e salvar manifesto

## Logica - Modo Verify

1. Carregar manifesto existente
2. Verificar hash do manifesto para detectar adulteracao
3. Para cada arquivo listado no manifesto:
   - Recalcular hash atual
   - Comparar com hash registrado
   - Marcar como PASS (identico) ou FAIL (diferente) ou MISSING
4. Gerar relatorio de verificacao

## Output - Generate

```
Evidence Hashing Report
Date: 2026-03-06T14:30:00Z
Algorithm: SHA-256
Path: ENG-2026-015-portal/evidence/

Files hashed: 23
Total size: 145.2 MB

Manifest saved: evidence-manifest-2026-03-06.sha256
Manifest hash: a1b2c3d4...
```

## Output - Verify

```
Evidence Verification Report
Manifest: evidence-manifest-2026-03-06.sha256
Manifest integrity: PASS

Results:
  PASS: 22 files
  FAIL: 1 file (FIND-007-screenshot-03.png - hash mismatch)
  MISSING: 0 files

WARNING: 1 file failed verification. Investigate immediately.
```

## Uso

```
evidence-hasher --path ./evidence/ --algorithm sha256 --mode generate
evidence-hasher --manifest evidence-manifest.sha256 --mode verify
```

## Boas Praticas

- Gerar hashes imediatamente apos coleta de evidencias
- Armazenar manifesto separado das evidencias
- Usar SHA-256 como minimo; SHA-512 para evidencias juridicas
- Nunca modificar evidencias apos hashing
