
# Modelo de Dados e Dicionário

## 1. Modelo Entidade-Relacionamento Flexível (Polimorfismo)
A arquitetura de dados suporta fluxos variáveis (Histopatológico, Citologia, Congelação e Imunohistoquímica) utilizando uma tabela auto-referenciada para permitir pulos de etapas físicas.

```mermaid
erDiagram
    AGHU_CACHE ||--o{ EXAME_PATHOTRACK : possui
    AGHU_CACHE {
        string numero_solicitacao
        string nome_paciente
        string prontuario
    }
    
    EXAME_PATHOTRACK ||--o{ PECA_FISICA : gera
    EXAME_PATHOTRACK {
        uuid id_exame
        string tipo_exame "Histopatologico, Citologia, Imuno"
        string status_global
    }

    PECA_FISICA ||--o{ PECA_FISICA : clivada_de
    PECA_FISICA {
        uuid id_peca
        string codigo_interno "Gerado pelo PathoTrack"
        string codigo_terceiros "Etiqueta Externa (Imuno)"
        string tipo_peca "Frasco, Cassete, Bloco, Lamina"
        uuid id_peca_pai "Self-referencing FK"
        string status_localizacao
        datetime data_registro
    }

    MENSAGEM_RETRABALHO ||--|| PECA_FISICA : refere_se_a
    MENSAGEM_RETRABALHO {
        uuid id_mensagem
        string medico_crm
        string conteudo_mensagem
        boolean lida
    }
```

## 2. Regras de Integridade e Vantagens Arquiteturais

    * Self-Referencing Table (PECA_FISICA): Evita rigidez.

        * Histopatológico: Lâmina (pai: Bloco) -> Bloco (pai: Cassete) -> Cassete (pai: Frasco).

        * Citologia Líquida: Lâmina (pai: Frasco) -> Sistema aceita a relação.

        * Citologia Cérvico-Vaginal: Lâmina (pai: NULL, ligada direto ao exame).

    * Código de Terceiros: A coluna codigo_terceiros permite salvar a etiqueta gerada por equipamentos automatizados de Imunohistoquímica.

    * Imutabilidade: A exclusão física (DELETE) é proibida. Uso obrigatório de Soft Delete (status "Descartada").