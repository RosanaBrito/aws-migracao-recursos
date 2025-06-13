# 📄 Documentação de Migração de Recursos AWS Entre Contas

## 🔁 Contexto
Migração completa de infraestrutura entre duas contas AWS, envolvendo serviços críticos de produção e desenvolvimento. A migração incluiu alterações de DNS, replicações de dados, ajustes de configuração e sincronização de serviços.

---

## ✅ Serviços e Recursos Envolvidos

- **Amazon EC2**
  - Instâncias de aplicações e serviços diversos
  - Elastic IPs
  - AMIs customizadas

- **Elastic Load Balancer (ALB)**
  - Load Balancers de produção e desenvolvimento
  - Edição de listeners e certificados SSL

- **Amazon RDS**
  - Criação de snapshots
  - Compartilhamento de snapshots entre contas
  - Criação de nova instância a partir do snapshot
  - Atualização de URLs e credenciais no backend

- **Amazon EFS**
  - Replicação entre contas
  - Desativação de proteções
  - Finalização e deleção pós-migração

- **AWS Secrets Manager**
  - Atualização de segredos utilizados pelas aplicações

- **Amazon Route 53 / DNS externo**
  - Troca de CNAMEs em provedores DNS externos (ex: iPages)
  - Redirecionamento para novas ALBs

- **Serviços Web (Nginx / Apache)**
  - Atualização de arquivos de configuração de frontend e backend
  - Alterações em arquivos de ambiente (.env, appsettings.json, environment.ts, etc)

- **Docker**
  - Reconstrução e subida de containers via `docker compose up -d --build`

---

## 🧭 Passos Seguidos na Migração

1. Planejamento e checklist por serviço
2. Criação e compartilhamento de snapshots (RDS)
3. Replicação de sistema de arquivos (EFS)
4. Cópia e permissão de AMIs personalizadas
5. Configuração de Security Groups e Roles de replicação
6. Desligamento de serviços nas contas antiga e nova
7. Alteração dos registros DNS nos servidores e provedores externos
8. Edição de arquivos de configuração nas aplicações
9. Atualização de Secrets Manager com novas credenciais
10. Reconstrução de aplicações com Docker
11. Associação de Elastic IPs
12. Testes finais e validação dos sistemas
13. Finalização e remoção de recursos antigos

---

## 🕒 Resumo da Linha do Tempo da Migração

- Desligamento dos serviços: ~21:15
- Snapshots e replicações: entre 21:22 e 22:11
- Criação de novos recursos e ajustes: até 23:25
- Sistemas de pé: até 00:30 (incluindo correção de imagem incorreta no BookStack)

---

## ✅ Observações Importantes

- Garantida a replicação segura de EFS e RDS
- Alterações de DNS planejadas e executadas na “hora da virada”
- Correções emergenciais aplicadas em tempo real (ex: imagem do BookStack)
- Todos os recursos finais estão na nova conta, com DNS atualizado e serviços ativos
