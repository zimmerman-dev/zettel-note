#### 🎨 Diagram: Types Hierarchy 
 ♻️ (*MinGW, Windows11, Codelite*)   
 ⌚7:34 pm  📆 Mon Jul 28
 🔗 **Related Concepts**: #cpp #diagram
___
```mermaid
flowchart TD
    %% Nodes
    B[bool]
    C[char]
    S[short]
    I[int]
    UI[unsigned int]
    L[long]
    UL[unsigned long]
    LL[long long]
    ULL[unsigned long long]
    F[float]
    D[double]
    LD[long double]

    %% Promotion chain (solid vertical arrows)
    B --> C
    C --> S
    S --> I
    I --> UI
    UI --> L
    L --> UL
    UL --> LL
    LL --> ULL
    ULL --> F
    F --> D
    D --> LD

    %% Integer -> Float auto promotions (angled solid arrows)
    I -->|auto-promote| F
    UI -->|auto-promote| F
    L -->|auto-promote| F
    UL -->|auto-promote| F
    LL -->|auto-promote| F
    ULL -->|auto-promote| F

    %% Demotion paths (dotted upward arrows)
    LD -.-> D
    D -.-> F
    F -.-> I
    ULL -.-> LL
    LL -.-> UL
    UL -.-> L
    L -.-> I
    UI -.-> I
    I -.-> S
    S -.-> C
    C -.-> B
```

- `-->` **Promotion** (automatic widening, safe)
    
- `..>` **Demotion** (narrowing, explicit cast required, may lose data)