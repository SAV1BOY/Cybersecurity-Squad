# Network Segmentation Designs

Padroes de segmentacao de rede para reducao de blast radius e lateral movement.

## Modelo de Zonas de Seguranca

```
[Internet] <-> [DMZ] <-> [Application Zone] <-> [Data Zone]
                              |
                        [Management Zone]
                              |
                        [Security Zone]
```

### Regras entre Zonas
- Internet -> DMZ: Apenas portas publicadas (443, 80)
- DMZ -> App Zone: Apenas portas de aplicacao especificas
- App Zone -> Data Zone: Apenas portas de database especificas
- Management Zone: Acesso restrito via jump host/bastion
- Security Zone: Isolada, acesso apenas para time de seguranca

## Micro-Segmentacao

**Abordagem tradicional:** Segmentacao por VLANs e firewalls
**Abordagem moderna:** Segmentacao por identidade e labels (workload-based)

### Implementacao com Service Mesh
```yaml
apiVersion: security.istio.io/v1
kind: AuthorizationPolicy
metadata:
  name: payment-service-policy
spec:
  selector:
    matchLabels:
      app: payment-service
  rules:
  - from:
    - source:
        principals: ["checkout-service"]
    to:
    - operation:
        methods: ["POST"]
        paths: ["/api/charge"]
```

## Segmentacao para Active Directory

- Tier 0: Domain Controllers, PKI, AD FS (maximo isolamento)
- Tier 1: Servidores de aplicacao e banco de dados
- Tier 2: Workstations e dispositivos de usuario
- Regra: Credenciais de tier superior nunca autenticam em tier inferior

## Validacao de Segmentacao

- Vulnerability scan cross-zone para verificar isolamento
- Purple team exercises para testar lateral movement
- Network traffic analysis para identificar comunicacoes nao autorizadas
