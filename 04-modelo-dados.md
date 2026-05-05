# Modelo de Dados e Dicionário

## 1. Modelo Entidade-Relacionamento
```mermaid
erDiagram
    PACIENTE ||--o{ PRONTUARIO : possui
    PACIENTE {
        string nome
        string cpf
        string cns
        date data_nascimento
    }
    PRONTUARIO ||--|{ EVOLUCAO : contem
    PRONTUARIO {
        int id
        datetime data_criacao
    }
    EVOLUCAO {
        string descricao
        string responsavel_crm
    }
```

## 2. Dicionário de Dados
* Tabela PACIENTES, PRONTUARIOS, etc.

## 3. Regras de Integridade
* Logs obrigatórios e proibição de exclusão física.
