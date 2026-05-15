# Arquitetura e Segurança

## 1. Stack Técnica (Baseado no Framework appstart)
* **Front-end**: Vue 3 com Vite e TypeScript (Interface reativa e componentes SPA).
* **Back-end**: Python com FastAPI (Alta performance, rotas assíncronas).
* **Banco de Dados**: PostgreSQL (Persistência local das peças físicas).

## 2. Integração e Padrões Arquiteturais
* **Arquitetura de Provedores**: A aplicação utiliza interfaces e injeção de dependência na camada de `providers`. A comunicação com o AGHU legada será isolada em um Provedor específico que atua como **Anti-Corruption Layer (ACL)**.
* **Cache Local Estratégico**: Para evitar paralisações na UACAP em caso de indisponibilidade da rede do HC, os dados demográficos do paciente retornados do AGHU na triagem são cacheados no PostgreSQL local.
* **Mensageria**: Uso de WebSockets no FastAPI para tráfego assíncrono de notificações de pedidos de "Retrabalho" do patologista para a bancada técnica.

## 3. Conformidade LGPD e Acessos
* Autenticação Híbrida: Suporte nativo ao Active Directory (AD) em produção para acesso unificado das credenciais dos profissionais, conforme infraestrutura do `appstart`.
* Auditoria rígida das consultas aos dados dos prontuários cruzados.

## 4. Guardrails para IA (SDD)
### Escopo Positivo (O que fazer)
- **Design Pattern**: Respeitar a divisão `routers` -> `controllers` -> `providers` exigida pelo framework.
- **Testes**: Criar rotinas de validação no fluxo de leitura da pistola de código de barras.

### Escopo Negativo (O que NÃO fazer - Anti-Patterns)
- **No Direct Legacy DB Queries**: O backend nunca deve executar instruções SQL diretamente contra as tabelas do AGHU; deve utilizar sempre os endpoints HTTP disponibilizados pela TI do hospital.