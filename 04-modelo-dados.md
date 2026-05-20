# Modelo de Dados e Dicionário

## 1. Modelo Entidade-Relacionamento
A estrutura foca na árvore hierárquica das amostras físicas, mantendo apenas o identificador da solicitação do AGHU para relacionamentos externos.
*(Está em processo de desenvolvimento - esperando validação total da solução proposta)*

```mermaid
erDiagram
    AGHU_CACHE ||--o{ FRASCO : gera
    AGHU_CACHE {
        string numero_solicitacao
        string nome_paciente
        string prontuario
        datetime data_cache
    }
    FRASCO ||--o{ CASSETE : clivado_em
    FRASCO {
        uuid id_frasco
        string codigo_interno
        datetime data_recepcao
    }
    CASSETE ||--o{ BLOCO : embutido_em
    CASSETE {
        uuid id_cassete
        string letra_fragmento
        string status_fase
    }
    BLOCO ||--o{ LAMINA : cortado_em
    BLOCO {
        uuid id_bloco
        datetime data_inclusao
    }
    LAMINA {
        uuid id_lamina
        string coloracao
        string status_laudo
    }
```

## 2. Dicionário de Dados
* Tabela PACIENTES, PRONTUARIOS, etc.

### [SCHEMA] Esquema JSON - Paciente
*Exemplo!*
```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "title": "Paciente",
  "type": "object",
  "properties": {
    "nome": { "type": "string", "minLength": 3 },
    "cpf": { "type": "string", "pattern": "^[0-9]{11}$" },
    "cns": { "type": "string", "pattern": "^[0-9]{15}$" },
    "data_nascimento": { "type": "string", "format": "date" }
  },
  "required": ["nome", "cpf", "data_nascimento"]
}
```

## 3. Regras de Integridade
* Logs obrigatórios e proibição de exclusão física.
