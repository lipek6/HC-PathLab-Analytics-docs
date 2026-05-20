# Especificação de Requisitos

## 1. Requisitos Funcionais (RF)
| ID | Título | Descrição | Prioridade |
| :--- | :--- | :--- | :--- |
| RF001 | Integração AGHU (ACL) | Consulta síncrona de pacientes e solicitações no AGHU via Camada Anticorrupção. | Essencial |
| RF002 | Gestão de Rastreabilidade Dinâmica | Geração de identificadores únicos adaptáveis ao tipo de exame (Histopatológico, Citologia, Congelação). | Essencial |
| RF003 | Visão Unificada | Exibição consolidada da árvore de clivagem local e dados clínicos do paciente. | Essencial |
| RF004 | Mensageria de Retrabalho | Notificações em tempo real (WebSockets) entre Microscopia e Processamento Técnico. | Alta |
| RF005 | Interface de Imunohistoquímica | Capacidade de ler e vincular etiquetas geradas por equipamentos automatizados de terceiros. | Alta |
| RF006 | Dashboard Operacional | Painel de controle de prazos (TAT) e status de liberação por processo. | Média |

## 2. Requisitos Não Funcionais (RNF)
| ID | Categoria | Descrição |
| :--- | :--- | :--- |
| RNF001 | Arquitetura | O backend (FastAPI) não pode realizar escrita no AGHU. Acesso estritamente Read-Only. |
| RNF002 | Resiliência | Cache local temporário de dados do paciente no PostgreSQL para contornar quedas de rede. |
| RNF003 | UI/UX | Interface em Vue 3 otimizada para uso direto com pistola de código de barras (HID). |

## 3. Detalhamento SDD (Padrão CARE)

### [CARE-RF002] Gestão de Rastreabilidade Dinâmica
* **Context**: O material recebido pode ter naturezas diferentes, exigindo fluxos distintos de clivagem.
* **Action**: Implementar motor de registro onde a criação de "itens filhos" depende do tipo de exame (ex: Citologia Cérvico-Vaginal gera Lâminas diretas, sem Cassetes/Blocos).
* **Result**: Geração de código interno preservando a árvore correta para a peça.
* **Evaluation**: Testes unitários devem validar a criação de Lâminas órfãs de Blocos em fluxos de Citologia.

### [CARE-RF004] Mensageria de Retrabalho via WebSockets
* **Context**: Médico patologista detecta necessidade de novos cortes durante análise microscópica.
* **Action**: Médico aciona "Solicitar Retrabalho" na Visão Unificada, gerando evento via WebSocket.
* **Result**: Bancadas do Processamento Técnico recebem notificação visual assíncrona contendo o ID do Bloco e a instrução técnica.
* **Evaluation**: Garantir propagação da notificação via `socket.io` em menos de 2 segundos.