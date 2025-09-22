# control-temperatura-en-lenguage-mermaid
control temperarura usando solo componentes pasivos un termistor y un 555

```mermaid
 graph TD
    subgraph "Fuente de Alimentación"
        A[Cargador USB 5V/2A] --> B(Regulador LM7805)
        B --> C(Salida +5V)
    end

    subgraph "Divisor de Voltaje y Sensado"
        C --> D[Resistencia Fija]
        D --> E(Termistor NTC)
        E --> F(GND)
    end

    subgraph "Comparador y Referencia"
        C --> H[Potenciómetro P_ref]
        H --> I[Entrada + del LM393]
        E --> G[Entrada - del LM393]
        I & G --> K[Comparador LM393]
    end

    subgraph "Generador de PWM (555 Astable)"
        K --> L(Pin 5 - Control)
        C --> M(Pin 8 - Vcc)
        M --> N(Pin 4 - Reset)
        N --> O(Pin 7 - Descarga)
        O --> P(Resistencia de PWM)
        P --> Q(Pin 6 - Umbral)
        P --> R(Pin 2 - Disparo)
        Q --> S(Condensador C1)
        S --> F
        R --> F
        L --> V(Pin 3 - Salida PWM)
    end

    subgraph "Etapa de Potencia"
        V --> W(Resistencia de Gate)
        W --> X(Gate del MOSFET)
        X --> Y(MOSFET IRF540)
        C --> Z(Carga Resistiva)
        Z --> AA(Drenador del MOSFET)
        Y --> AB(Fuente del MOSFET)
        AB --> F
    end

    style F fill:#ffccbc,stroke:#333,stroke-width:2px;
