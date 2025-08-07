```mermaid
graph TD
    %% Définition des acteurs sous forme de "swimlanes" (couloirs)

    subgraph Pilote Normalisation
        A(Initier le workflow<br>Renseigner infos normatives);
        D{Complément d'info?};
    end

    subgraph Responsable BE
        C1(Analyse par Resp. BE);
    end
    
    subgraph Responsable Tests R&D
        C2(Analyse par Resp. Tests R&D);
        J(Assigner les essais);
    end

    subgraph Technicien Tests R&D
        K{Prototypes disponibles?};
        L(Réaliser essais partiels);
        M(Réaliser essais complets);
        N(Mise en stand-by<br>pour futurs prototypes);
    end

    subgraph Réunion SAP Tech (Instance de décision)
        E(SAP Tech 1: Évaluation de l'impact);
        F{Quel est l'impact potentiel?};
        H(Plan d'action initial<br>Lobbying, Modif...);
        O(SAP Tech 2: Débriefing<br>des résultats);
        P{Débriefing final?};
        Q{Conclusion finale?};
        S(Plan d'action final);
    end

    subgraph Fin du Processus
        G([Fin du workflow]);
        I([Fin du workflow]);
        R([Fin du workflow]);
        T([Fin du workflow]);
    end

    %% Connexions du workflow entre les acteurs
    A --> B{Type d'évolution?};
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

    %% Style (optionnel, mais améliore la lisibilité)
    classDef decision fill:#e6f2ff,stroke:#0066cc;
    classDef meeting fill:#fff0b3,stroke:#ff9900;
    classDef endNode fill:#e6ffe6,stroke:#009900;
    class B,D,F,K,P,Q decision;
    class E,H,O,S meeting;
    class G,I,R,T endNode;
