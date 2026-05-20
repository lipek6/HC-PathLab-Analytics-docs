# Interfaces e Integrações

## 1. UI / UX (Frontend)
* Single Page Application (SPA) construída em **Vue.js 3**.
* Navegação em abas: *Leitura e Rastreio*, *Dashboard Operacional* e *Registro de Peças*.
* Captura otimizada de eventos globais de teclado (Keypress events) para permitir uso de pistola de leitura sem necessidade de focar o cursor em um input específico.

## 2. Integração de Hardware
* **Leitores Ópticos**: Pistolas leitoras operando em emulação de teclado (HID) para escanear etiquetas internas e etiquetas externas (Imunohistoquímica).
* **Agente de Impressão Local (`localhost`)**: Serviço rodando em *background* nas máquinas das bancadas para contornar o *sandbox* do navegador e enviar comandos diretos.
* **Impressoras Térmicas**: Comunicação via rede local/USB utilizando linguagem ZPL (Zebra Programming Language) para plotagem de QR Codes em cassetes plásticos e lâminas de vidro.

## 3. Interface de Integração (Camada Anticorrupção)
Integração *Read-Only* ao AGHU abstraída no Backend (FastAPI).

### [SCHEMA] Interface de Integração AGHU (Python/FastAPI Provider)
```python
class AGHUIntegrationProvider(ABC):
    @abstractmethod
    async def get_patient_by_solicitation(self, request_id: str) -> PatientRecord:
        pass

    @abstractmethod
    async def get_macroscopy_text(self, request_id: str) -> str:
        pass