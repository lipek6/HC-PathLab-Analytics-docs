# Documento de Visão

## 1. Problema e Oportunidade
* **O Problema**: O sistema AGHU possui granularidade limitada no Módulo de Exames, sendo incapaz de gerenciar o ciclo de vida dos subprodutos físicos de uma peça patológica (cassetes e lâminas).
* **Impacto**: A dependência de planilhas Excel paralelas e Fichas de Trabalho em papel gera alto risco de perda de amostras, erros de transcrição, troca de identificações e incapacidade de rastrear o SLA (Turnaround Time) em tempo real.
* **Solução Proposta**: O PathoTrack atua como a única fonte da verdade para o mapeamento físico da amostra, gerando etiquetas exclusivas. Ao ler a etiqueta, o sistema provê uma "Visão Unificada", cruzando o histórico físico local com os dados médicos importados em tempo real do AGHU.

## 2. Partes Interessadas (Stakeholders)
* **Usuários Finais**: Técnicos de laboratório, Macroscopistas, Médicos Patologistas, Residentes.
* **Gestão**: Recepcionistas, Coordenação da UACAP.

## 3. Escopo do Produto
* Motor de registro de clivagem (geração 1:N de cassetes e lâminas).
* Dashboard operacional de controle de tempo e gargalos.
* Integração para impressão direta de etiquetas térmicas (Zebra/Argox).
* **Fora de Escopo**: O sistema não será repositório legal de laudos, que continuarão sendo redigidos e liberados nativamente no AGHU.

## 4. Metas e Objetivos de Negócio
* Zerar a taxa de perda/troca de identificação de amostras.
* Eliminar 100% o uso da "Ficha de Trabalho" impressa transitando pelo laboratório.
* Reduzir o tempo gasto em busca ativa de peças e controle de prazos manuais.