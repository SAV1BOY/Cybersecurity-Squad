# AppSec - Serverless Security

Checklist para seguranca de aplicacoes serverless.

## Function Configuration
- [ ] IAM role per function com least privilege
- [ ] Memory e timeout limits definidos adequadamente
- [ ] Environment variables sem secrets em plaintext
- [ ] VPC configuration quando acesso a recursos internos necessario
- [ ] Concurrency limits definidos para prevenir abuse
- [ ] Dead letter queues configuradas para error handling
- [ ] Function layers auditadas para vulnerabilidades

## Authentication e Authorization
- [ ] API Gateway authentication configurada (Cognito, JWT, API Key)
- [ ] Function-level authorization implementada
- [ ] IAM policies granulares por function
- [ ] Cross-account access restrito e auditado
- [ ] Service-to-service auth implementado (IAM roles, tokens)
- [ ] Public access restrito apenas a endpoints necessarios
- [ ] CORS configurado restritivamente

## Input Validation
- [ ] API Gateway request validation habilitada
- [ ] Input validation implementada dentro da function
- [ ] Event source validation (trigger legitimacy verified)
- [ ] Injection prevention para todos os inputs
- [ ] Payload size limits definidos
- [ ] Schema validation para request/response

## Data Security
- [ ] Encryption at rest para dados armazenados
- [ ] Encryption in transit para comunicacao entre services
- [ ] Temporary files limpos apos execucao
- [ ] /tmp directory nao usado para dados persistentes sensiveis
- [ ] KMS keys com access control adequado
- [ ] Sensitive data nao logada em CloudWatch/console

## Dependency e Runtime Security
- [ ] Dependencies minimizadas (menos attack surface)
- [ ] Dependencies scanned para vulnerabilidades
- [ ] Runtime atualizado para versao suportada
- [ ] Custom runtime hardened (se utilizado)
- [ ] Layer dependencies auditadas e pinadas
- [ ] Function code obfuscated se necessario (IP protection)

## Logging e Monitoring
- [ ] Structured logging implementado em cada function
- [ ] CloudWatch/equivalent metrics configuradas
- [ ] Alerting para errors e anomalies configurado
- [ ] Distributed tracing implementado (X-Ray, Jaeger)
- [ ] Cold start performance monitorada
- [ ] Cost monitoring para detectar abuse (cryptomining, etc.)
- [ ] Invocation patterns monitorados para anomalias

## Event Source Security
- [ ] Event sources autenticadas e autorizadas
- [ ] S3 event triggers com bucket policy restritiva
- [ ] SQS/SNS message validation implementada
- [ ] DynamoDB streams com access control adequado
- [ ] Schedule triggers revisados para necessidade
- [ ] Webhook endpoints protegidos com signature validation
- [ ] Report de seguranca serverless entregue
