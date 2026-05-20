# Documento de Visão

## 1. Problema e Oportunidade
* **O Problema**: O sistema AGHU possui granularidade limitada no Módulo de Exames, não suportando o rastreio da clivagem de peças e as variações de fluxo da UACAP (Citologia, Congelação, Histopatológico e Imunohistoquímica).
* **Impacto**: A dependência de planilhas Excel paralelas e Fichas de Trabalho em papel gera alto risco de perda de amostras, erros de transcrição e falta de controle do SLA (Turnaround Time).
* **Solução Proposta**: O PathoTrack atua como fonte da verdade flexível para o mapeamento físico. Gerando etiquetas exclusivas (e adotando etiquetas de terceiros), o sistema provê uma "Visão Unificada" na tela ao cruzar a árvore física local com os dados médicos importados do AGHU (*Read-only*).

## 2. Partes Interessadas (Stakeholders)
* **Usuários Finais**: Técnicos de laboratório, Macroscopistas, Médicos Patologistas, Residentes e Citopatologistas.
* **Gestão**: Recepcionistas, Coordenação da UACAP e TI do HC.

## 3. Escopo do Produto
* Motor flexível de registro de clivagem (capaz de pular fases como cassetes/blocos dependendo do tipo de material).
* Dashboard operacional de controle de tempo e gargalos.
* Integração via Agente Local para impressão de etiquetas térmicas (Zebra/Argox) e suporte a leitores de código de barras.
* Mensageria em tempo real para solicitação de retrabalho técnico.
* **Fora de Escopo**: O sistema não será repositório legal de laudos, que continuarão sendo redigidos e liberados nativamente no AGHU.

## 4. Metas e Objetivos de Negócio
* Zerar a taxa de perda/troca de identificação de amostras.
* Eliminar 100% o uso da "Ficha de Trabalho" impressa transitando pelo laboratório.
* Garantir suporte arquitetural a todos os fluxos atípicos (Biópsia de Congelação, Citologia).