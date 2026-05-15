# SPEC.md - Contrato de Desenvolvimento (SDD)

## 1. Visão Geral e Resultados Esperados
Este documento é a ÚNICA fonte de verdade para a orquestração do desenvolvimento. O objetivo é construir o PathoTrack, um sistema satélite seguro, integrado em modo read-only ao AGHU, para rastreabilidade física de amostras patológicas.

### Objetivos de Alto Nível
- [ ] Implementar autenticação via LDAP/AD (utilizando o módulo auth do framework appstart).
- [ ] Gerenciar a árvore de clivagem biológica (Frasco -> Cassete -> Bloco -> Lâmina).
- [ ] Integrar leitura de pacientes do AGHU via Camada Anticorrupção (ACL).
- [ ] Garantir trilhas de auditoria para cada transição de fase da peça física.

## 2. Contexto do Projeto (Documentação Imutável)
As definições detalhadas estão distribuídas nos seguintes documentos:
- [Visão](01-visao.md)
- [Requisitos](02-requisitos.md)
- [Casos de Uso](03-casos-uso.md)
- [Modelo de Dados](04-modelo-dados.md)
- [Interfaces](05-interfaces.md)
- [Arquitetura](06-arquitetura.md)
- [Glossário](07-glossario.md)

## 3. Limites de Escopo e Guardrails (Anti-Patterns)
**A IA DEVE:**
- Seguir rigorosamente o Modelo de Dados definido em `04-modelo-dados.md`.
- Utilizar a *Arquitetura de Provedores* do `appstart` para qualquer integração de dados.
- Implementar testes unitários focados na árvore de clivagem.

**A IA NÃO DEVE:**
- Criar dependências externas de escrita no banco do AGHU (Acesso estritamente *Read-Only*).
- Implementar exclusão física de registros de amostras (usar Soft Delete/Status "Descartado").
- Burlar o sistema de RBAC para acesso a laudos de pacientes sensíveis.

## 4. Task Breakdown (Plano de Implementação)
### Fase 1: Infraestrutura e Dados
- [ ] [TASK-001] Modelar entidades no SQLAlchemy (Frasco, Cassete, Bloco, Lamina).
- [ ] [TASK-002] Configurar provedor Mock de Autenticação para desenvolvimento local.

### Fase 2: Integração e Domínio
- [ ] [TASK-003] Criar Interface do Provider de Integração com o AGHU (ACL).
- [ ] [TASK-004] Implementar endpoints de geração de códigos internos ZPL para impressão.