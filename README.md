```mermaid
graph TD
    classDef decision fill:#e6f2ff,stroke:#0066cc;
    classDef process fill:#f0f0f0,stroke:#555;
    classDef meeting fill:#fff0b3,stroke:#ff9900;
    classDef endNode fill:#e6ffe6,stroke:#009900;

    subgraph Phase 1 Initialisation
        A(Initier le workflow<br>Renseigner infos normatives):::process;
        B{Type d'évolution?}:::decision;
        C1(Analyse par Resp. BE):::process;
        C2(Analyse par Resp. Tests R&D):::process;
        D{Complément d'info?}:::decision;
    end

    subgraph Phase 2 SAP Tech - Évaluation
        E(SAP Tech 1: Évaluation de l'impact):::meeting;
        F{Quel est l'impact potentiel?}:::decision;
        G([Fin du workflow]):::endNode;
        H(Plan d'action initial<br>Lobbying, Modif...):::process;
        I([Fin du workflow]):::endNode;
    end

    subgraph Phase 3 Essais R&D
        J(Assigner les essais):::process;
        K{Prototypes disponibles?}:::decision;
        L(Réaliser essais partiels):::process;
        M(Réaliser essais complets):::process;
        N(Mise en stand-by<br>pour futurs prototypes):::process;
    end

    subgraph Phase 4 SAP Tech - Débriefing
        O(SAP Tech 2: Débriefing<br>des résultats):::meeting;
        P{Débriefing final?}:::decision;
        Q{Conclusion finale?}:::decision;
        R([Fin du workflow]):::endNode;
        S(Plan d'action final):::process;
        T([Fin du workflow]):::endNode;
    end
    
    A --> B;
    B -- Exigence de performance --> C1;
    B -- Méthode d'essai --> C2;
    C1 --> D;
    C2 --> D;
    D -- Oui --> A;
    D -- Non --> E;
    E --> F;
    F -- Absence d'impact --> G;
    F -- Impact avéré --> H;
    H --> I;
    F -- Impact à vérifier --> J;
    J --> K;
    K -- Non --> L;
    K -- Oui --> M;
    L --> O;
    M --> O;
    O --> P;
    P -- Non (partiel) --> N;
    N --> K;
    P -- Oui (final) --> Q;
    Q -- Absence d'impact --> R;
    Q -- Impact confirmé --> S;
    S --> T;
