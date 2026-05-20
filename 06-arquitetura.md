### `06-arquitetura.md`
```markdown
# Arquitetura e Decisões Técnicas

## 1. Padrões Arquiteturais e Guardrails
O sistema adota a **Arquitetura Hexagonal (Ports & Adapters)** no backend para garantir o isolamento absoluto das regras de negócio (Anatomia Patológica) em relação a dependências externas (como o sistema legado AGHU e drivers de hardware).

**Guardrails de Integração:**
* **Read-Only no Legado:** O PathoTrack atua com acesso estritamente de leitura ao AGHU via Camada Anticorrupção (ACL).
* **Master Data:** O AGHU é a fonte da verdade para dados do paciente. O banco local (PostgreSQL) é a fonte da verdade exclusiva para a linhagem física (cassetes/lâminas/blocos).

## 2. Stack Tecnológica (Framework HC-UFPE)
O desenvolvimento utiliza o repositório `appstart` disponibilizado pelo HC:

* **Frontend:** SPA em **Vue.js 3** com Vite.
* **Backend:** **Python com FastAPI** para alta performance e suporte nativo assíncrono.
* **Banco de Dados:** **PostgreSQL** para persistência relacional do histórico físico e estruturação hierárquica.

## 3. Componentes de Comunicação
* **Anti-Corruption Layer (ACL):** Componente do FastAPI dedicado a consultar o Módulo de Exames do AGHU e implementar cache local (*fallback*) em caso de indisponibilidade de rede, mantendo a operação da UACAP ininterrupta.
* **Tempo Real (WebSockets):** Conexões bidirecionais suportadas pelo FastAPI para envio de solicitações de retrabalho do médico para as bancadas técnicas.
* **Tráfego Assíncrono Híbrido:** Requisições transacionais (`GET/POST` bipagem) operam via HTTP síncrono. Comandos de impressão operam de forma assíncrona para não onerar a *thread* principal do usuário.