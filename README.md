```mermaid
graph TD
    %% Définition des couloirs pour chaque acteur
    subgraph Pilote_Normalisation
        A("Initier le workflow<br>Renseigner infos normatives");
        D{"Complément d'info?"};
    end

    subgraph Responsable_BE [Pilote SAP Tech]
        C1("Analyse pré-SAP Tech");
        E("SAP Tech 1: Évaluation de l'impact");
        F{"Quel est l'impact potentiel?"};
        H("Plan d'action initial<br>Lobbying, Modif...");
        O("SAP Tech 2: Débriefing<br>des résultats d'essais");
        P{"Débriefing final?"};
        Q{"Conclusion finale?"};
        S("Plan d'action final");
    end
    
    subgraph Responsable_Tests_RD
        C2("Analyse pré-SAP Tech");
        J("Assigner les essais");
    end

    subgraph Technicien_Tests_RD
        K{"Prototypes disponibles?"};
        L("Réaliser essais partiels");
        M("Réaliser essais complets");
        N("Mise en stand-by<br>pour futurs prototypes");
    end

    subgraph Fin_Processus
        G(["Fin du workflow"]);
        I(["Fin du workflow"]);
        R(["Fin du workflow"]);
        T(["Fin du workflow"]);
    end

    %% Connexions du workflow
    A --> B{"Type évolution?"};
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

    %% Styles
    classDef decision fill:#e6f2ff,stroke:#0066cc;
    classDef meeting fill:#fff0b3,stroke:#ff9900;
    classDef endNode fill:#e6ffe6,stroke:#009900;
    class B,D,F,K,P,Q decision;
    class E,H,O,S meeting;
    class G,I,R,T endNode;
