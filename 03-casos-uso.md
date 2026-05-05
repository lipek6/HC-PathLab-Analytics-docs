# Modelagem de Casos de Uso

## 1. Diagrama de Casos de Uso
*(Inserir imagem ou Mermaid)*
```mermaid
useCaseDiagram
    actor "Enfermeiro" as E
    actor "Médico" as M
    
    package "Sistema Hospitalar" {
        usecase "Realizar Triagem" as UC1
        usecase "Consultar Histórico" as UC2
        usecase "Prescrever Medicamento" as UC3
    }
    
    E --> UC1
    E --> UC2
    M --> UC2
    M --> UC3
```

## 2. Especificação (Exemplo)
### UC001 - Triagem
* **Ator**: Enfermeiro.
* **Fluxo**: Selecionar paciente -> Inserir Sinais Vitais -> Calcular Manchester.
