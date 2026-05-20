# SPEC.md - Contrato de Desenvolvimento (SDD)

## 1. Visão Geral e Resultados Esperados
Este documento é a ÚNICA fonte de verdade para a orquestração do desenvolvimento. O objetivo é construir o PathoTrack, um sistema satélite seguro, integrado em modo read-only ao AGHU, para rastreabilidade física de amostras patológicas em múltiplos fluxos de processamento.

### Objetivos de Alto Nível
- [ ] Implementar autenticação híbrida via LDAP/AD (framework `appstart`).
- [ ] Gerenciar a árvore de clivagem biológica adaptável (Histopatológico, Citologia, Congelação e Imunohistoquímica).
- [ ] Integrar leitura de pacientes do AGHU via Camada Anticorrupção (ACL).
- [ ] Garantir trilhas de auditoria para cada transição de fase da peça física.

## 2. Contexto do Projeto (Documentação Imutável)
As definições detalhadas estão distribuídas nos seguintes documentos:
- [Visão](01-visao.md) | [Requisitos](02-requisitos.md) | [Casos de Uso](03-casos-uso.md) | [Modelo de Dados](04-modelo-dados.md) | [Interfaces](05-interfaces.md) | [Arquitetura](06-arquitetura.md) | [Glossário](07-glossario.md)

## 3. Limites de Escopo e Guardrails (Anti-Patterns)
**A IA DEVE:**
- Seguir rigorosamente o Modelo de Dados Polimórfico definido em `04-modelo-dados.md` (Tabela `PECA_FISICA` auto-referenciada).
- Utilizar a *Arquitetura de Provedores* do `appstart` para a integração com o AGHU.
- Implementar suporte para leitura de códigos de terceiros (equipamentos de imunohistoquímica).

**A IA NÃO DEVE:**
- Criar dependências externas de escrita no banco do AGHU (Acesso estritamente *Read-Only*).
- Engessar a criação de lâminas à existência obrigatória de blocos ou cassetes (fluxos de citologia pulam etapas).
- Implementar exclusão física de registros de amostras (usar Soft Delete/Status "Descartado").

## 4. Task Breakdown (Plano de Implementação)
### Fase 1: Infraestrutura e Dados
- [ ] [TASK-001] Modelar entidade polimórfica no SQLAlchemy (PecaFisica).
- [ ] [TASK-002] Configurar provedor Mock de Autenticação para desenvolvimento local.

### Fase 2: Integração e Domínio
- [ ] [TASK-003] Criar Interface do Provider de Integração com o AGHU (ACL).
- [ ] [TASK-004] Implementar motor de clivagem condicional e endpoints de geração ZPL.