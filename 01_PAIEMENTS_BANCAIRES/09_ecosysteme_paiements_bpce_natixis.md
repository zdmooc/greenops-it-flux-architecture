# 09 — Écosystème Paiements BPCE / Natixis / Banque Populaire / Caisse d’Épargne

## 1. Objectif du document

Ce document présente une vue d’architecture de l’écosystème paiements BPCE / Natixis à partir d’informations publiques et d’une lecture SI.

Il couvre :

- Groupe BPCE ;
- Banque Populaire ;
- Caisse d’Épargne ;
- Natixis / Natixis CIB / GTB ;
- BPCE Payment Services ;
- BPCE Digital & Payments ;
- Oney ;
- Wero / EPI ;
- API Store BPCE / PISP ;
- Estreem / processing carte ;
- infrastructures STET, TIPS, T2, SWIFT ;
- flux SCT, SDD, SCT Inst, cross-border, cash management, carte, paiement fractionné.

L’objectif n’est pas de décrire l’architecture interne réelle du groupe, qui n’est pas publique, mais de construire un **référentiel d’architecture plausible, structuré et exploitable** pour comprendre les flux paiements dans un contexte BPCE / Natixis.

---

## 2. Sources et limites

Ce document s’appuie sur des sources publiques :

- site Groupe BPCE ;
- BPCE Digital & Payments ;
- Natixis ;
- API Store Groupe BPCE ;
- newsroom Groupe BPCE ;
- STET ;
- Banque centrale européenne / TIPS ;
- Reuters pour Estreem ;
- documents publics liés à BPCE International / Océor.

Les schémas d’architecture sont des **modèles de compréhension**. Ils ne prétendent pas représenter une cartographie interne confidentielle.

---

## 3. Vue d’ensemble du Groupe BPCE

Le Groupe BPCE est le deuxième acteur bancaire en France. Il opère notamment les réseaux Banque Populaire et Caisse d’Épargne, ainsi que Banque Palatine et Oney. Le groupe sert environ 35 millions de clients dans le monde et réunit plus de 100 000 collaborateurs.

Dans le domaine des paiements, le groupe s’appuie sur plusieurs plaques :

- les réseaux Banque Populaire et Caisse d’Épargne pour la relation client, la banque de proximité, les applications mobiles et les usages quotidiens ;
- BPCE Payment Services comme opérateur industriel de paiements ;
- BPCE Digital & Payments comme pôle regroupant les expertises paiements, digital, IA, data, innovations et financement du commerce ;
- Natixis pour les métiers corporate, CIB, cash management, paiements internationaux et services financiers ;
- Oney pour le paiement fractionné et les solutions de financement ;
- Wero / EPI pour le paiement européen de compte à compte ;
- Estreem pour le processing carte à l’échelle européenne avec BNP Paribas ;
- les infrastructures de place STET, TIPS, T2 et SWIFT.

---

## 4. Vue macro de l’écosystème

```mermaid
flowchart TD
    BPCE[Groupe BPCE] --> BP[Banque Populaire]
    BPCE --> CE[Caisse d'Épargne]
    BPCE --> PAL[Banque Palatine]
    BPCE --> NAT[Natixis]
    BPCE --> BPS[BPCE Payment Services]
    BPCE --> DNP[BPCE Digital & Payments]
    BPCE --> ONEY[Oney]
    BPCE --> WERO[Wero / EPI]
    BPCE --> EST[Estreem]

    BP --> CLIENTS[Particuliers / Pros / Entreprises]
    CE --> CLIENTS
    PAL --> CLIENTS

    NAT --> CIB[Corporate / CIB / GTB]
    NAT --> XB[Cross-border / Cash Management]

    DNP --> BPS
    BPS --> SCT[SCT]
    BPS --> SDD[SDD]
    BPS --> INST[SCT Inst]
    BPS --> API[API / PISP]
    BPS --> CARD[Cartes / Monétique]

    ONEY --> BNPL[Paiement fractionné]
    WERO --> A2A[Paiement compte à compte]
    EST --> PROC[Processing carte]
```

---

## 5. Rôle des principales entités

### 5.1 Banque Populaire et Caisse d’Épargne

Les réseaux Banque Populaire et Caisse d’Épargne sont les points d’entrée clients majeurs pour :

- virements SCT ;
- virements instantanés SCT Inst ;
- prélèvements SDD ;
- paiements carte ;
- services digitaux ;
- Wero ;
- encaissement commerçant ;
- banque à distance ;
- services professionnels et entreprises.

Lecture architecture :

```text
Banque Populaire / Caisse d'Épargne
   =
front client
   +
canaux digitaux
   +
distribution des services paiement
   +
relation particuliers, pros et entreprises
```

Ces réseaux sont exposés aux usages opérationnels : paiement mobile, initiation de virement, notification, relevés, gestion des bénéficiaires, authentification forte, contestations et service client.

### 5.2 BPCE Payment Services

BPCE Payment Services est décrit publiquement comme l’opérateur industriel de paiements du Groupe BPCE. Il accompagne les banques et filiales du groupe ainsi que des clients externes sur les paiements, le processing, les solutions de paiement et les services connectés.

Lecture architecture :

```text
BPCE Payment Services
   =
usine à paiements
   +
processing industriel
   +
orchestration des flux
   +
services API
   +
monétique / cartes
   +
SCT / SDD / SCT Inst
```

Responsabilités typiques dans une lecture SI :

- réception de flux ;
- contrôle et enrichissement ;
- transformation de formats ;
- routage ;
- connexion aux infrastructures ;
- gestion des statuts ;
- supervision ;
- industrialisation ;
- qualité de service ;
- réduction des traitements inutiles.

### 5.3 BPCE Digital & Payments

BPCE Digital & Payments met en synergie les expertises de paiements, financement du commerce, digital, IA, data et innovations technologiques. Les données publiques 2025 indiquent notamment :

- plus de 3 000 collaborateurs en Europe ;
- n°1 du paiement fractionné en France avec Oney ;
- n°2 des paiements en France ;
- plus de 11 milliards de transactions de paiement par an ;
- plus de 30 millions de cartes gérées ;
- plus de 11 millions de clients actifs sur les applications mobiles Banque Populaire et Caisse d’Épargne.

Lecture architecture :

```text
BPCE Digital & Payments
   =
paiements
+
digital
+
data
+
IA
+
innovation
+
industrialisation des usages clients
```

Ces chiffres traduisent une volumétrie industrielle : le sujet paiement doit donc être traité comme une chaîne critique de production, avec performance, résilience, sécurité, observabilité et sobriété.

### 5.4 Natixis

Natixis présente les paiements comme des solutions “payment as a service” couvrant la chaîne de valeur : issuing, acquisition, omnicanal, processing et data.

Dans une lecture architecture, Natixis se positionne notamment sur :

- paiements corporate ;
- cash management ;
- paiements internationaux ;
- paiements multi-devises ;
- banque de financement et d’investissement ;
- clients institutionnels et grandes entreprises ;
- conventions de remise d’ordres ;
- intégration ERP / trésorerie ;
- SWIFT, EBICS, API et reporting.

Lecture architecture :

```text
Natixis
   =
corporate / CIB / GTB
   +
cash management
   +
cross-border
   +
multi-devises
   +
conformité internationale
```

### 5.5 Oney

Oney est une banque spécialisée dans les solutions de paiement et services financiers. Le Groupe BPCE a finalisé en 2019 l’acquisition de 50,1 % du capital d’Oney Bank aux côtés d’Auchan Holding.

Oney est structurant pour :

- paiement fractionné ;
- paiement en plusieurs fois ;
- BNPL ;
- scoring ;
- financement court terme ;
- intégration commerçants ;
- expérience client.

Lecture architecture :

```text
Oney
   =
paiement fractionné
+
scoring risque
+
crédit court terme
+
parcours commerçant
+
échéancier de remboursement
```

### 5.6 Wero / EPI

Wero est le portefeuille de paiement européen porté par EPI. Il s’appuie sur le paiement de compte à compte et le virement instantané. BPCE a annoncé les premières transactions Wero e-commerce en France et le déploiement du service aux clients Banque Populaire et Caisse d’Épargne.

Lecture architecture :

```text
Wero
   =
wallet européen
+
paiement compte à compte
+
SCT Inst
+
authentification mobile
+
expérience temps réel
```

Wero transforme le SCT Inst en moyen de paiement du quotidien : P2P, e-commerce, mobile, puis potentiellement point de vente.

### 5.7 Estreem

Estreem est une coentreprise de BNP Paribas et BPCE dans le processing des paiements carte. Reuters indique que l’entité vise le traitement des paiements cartes de BNP Paribas et du Groupe BPCE en Europe, avec un volume annoncé de 17 milliards de transactions par an.

Lecture architecture :

```text
Estreem
   =
processing carte
+
industrialisation européenne
+
volumétrie massive
+
standardisation technologique
```

### 5.8 BPCE International / Océor

Océor renvoie historiquement aux participations internationales et outre-mer du groupe, ensuite regroupées dans BPCE International et Outre-mer, devenu BPCE International. Dans le cadre d’un référentiel paiements, ce point est utile pour comprendre l’héritage groupe autour :

- de la banque de détail à l’international ;
- des outre-mer ;
- des participations bancaires ;
- des flux internationaux ;
- des besoins de correspondance bancaire ;
- des transferts multi-pays et multi-devises.

Lecture architecture :

```text
Océor / BPCE International
   =
héritage international et outre-mer
+
réseaux bancaires hors métropole
+
flux internationaux
+
besoins cross-border
```

---

## 6. Cartographie des flux BPCE / Natixis

| Flux | Entités concernées | Infrastructure / support | Lecture architecture |
|---|---|---|---|
| SCT | Banque Populaire, Caisse d’Épargne, BPCE Payment Services | SEPA, STET / ACH | batch, volumétrie, cut-off |
| SDD | BP/CE, clients corporate, créanciers | SEPA, STET / ACH | mandat, R-transactions, retours |
| SCT Inst | apps BP/CE, Wero, BPCE Payment Services | TIPS / instant payment | temps réel, idempotence, retry |
| Cross-border | Natixis, CIB, corporate | SWIFT, correspondants | AML, sanctions, devises |
| Cash Management | Natixis GTB, entreprises | camt, EBICS, SWIFT, API | reporting, ERP, réconciliation |
| Carte | BPCE Digital & Payments, Estreem | processing carte | autorisation, clearing, settlement |
| Oney | commerçants, clients, BP/CE pros | carte, scoring, crédit | paiement fractionné, risque |
| PISP | API Store BPCE, BPCE Payment Services | API, SCT/SCT Inst | initiation, consentement, encaissement |
| Wero | BP/CE, EPI, clients mobiles | wallet, SCT Inst | compte à compte, mobile, e-commerce |

---

## 7. Vue fonctionnelle globale

```mermaid
flowchart TD
    subgraph Clients[Clients et usages]
        PART[Particuliers]
        PRO[Professionnels]
        CORP[Entreprises / Corporate]
        MERCH[Commerçants]
    end

    subgraph Canaux[Canaux]
        APPBP[App Banque Populaire]
        APPCE[App Caisse d'Épargne]
        API[API / PISP]
        EBICS[EBICS / Host-to-Host]
        SWIFTIN[SWIFT / fichiers corporate]
        WEROAPP[Wero]
    end

    subgraph Socle[Socle paiements groupe]
        BPS[BPCE Payment Services]
        HUB[Payment Hub]
        EAI[Middleware / EAI]
        AML[Fraude / AML / Sanctions]
        OBS[Observabilité]
        GREEN[GreenOps / SCI]
    end

    subgraph Traitements[Domaines paiements]
        SCT[SCT]
        SDD[SDD]
        INST[SCT Inst]
        XB[Cross-border]
        CASH[Cash Management]
        CARD[Carte]
        BNPL[Oney / Paiement fractionné]
    end

    subgraph Infrastructures[Infrastructures de place]
        STET[STET / ACH]
        TIPS[TIPS]
        T2[T2]
        SWIFT[SWIFT]
        EST[Estreem / processing carte]
    end

    PART --> APPBP
    PART --> APPCE
    PRO --> APPBP
    PRO --> APPCE
    CORP --> EBICS
    CORP --> API
    MERCH --> API
    PART --> WEROAPP

    APPBP --> BPS
    APPCE --> BPS
    WEROAPP --> BPS
    EBICS --> HUB
    API --> HUB
    SWIFTIN --> HUB

    BPS --> EAI
    HUB --> EAI
    EAI --> AML
    AML --> SCT
    AML --> SDD
    AML --> INST
    AML --> XB
    EAI --> CASH
    EAI --> CARD
    EAI --> BNPL

    SCT --> STET
    SDD --> STET
    STET --> T2
    INST --> TIPS
    XB --> SWIFT
    CARD --> EST

    EAI --> OBS
    OBS --> GREEN
```

---

## 8. Flux BPCE type — SCT classique

```mermaid
sequenceDiagram
    participant Client as Client BP/CE
    participant App as App Banque Populaire / Caisse d'Épargne
    participant BPS as BPCE Payment Services
    participant STET as STET / ACH
    participant T2 as T2
    participant BankB as Banque bénéficiaire
    participant Benef as Bénéficiaire

    Client->>App: Ordre de virement SCT
    App->>BPS: Transmission ordre
    BPS->>BPS: Validation ISO / métier / conformité
    BPS->>STET: pacs.008
    STET->>T2: Règlement position
    STET->>BankB: Instruction interbancaire
    BankB->>Benef: Crédit bénéficiaire
    STET-->>BPS: Statut / retour
    BPS-->>App: Statut client
```

### Points critiques

- qualité IBAN / BIC ;
- cut-off ;
- batchs volumineux ;
- fichiers rejetés ;
- rejets tardifs ;
- relances ;
- logs ;
- réconciliation.

### Lecture GreenOps

Le SCT produit du carbone surtout via :

- batchs lourds ;
- retraitements ;
- replays ;
- logs complets ;
- stockage de fichiers ;
- transformations multiples.

---

## 9. Flux BPCE type — SDD

```mermaid
sequenceDiagram
    participant Cred as Créancier
    participant BPS as BPCE Payment Services
    participant Mandat as Référentiel mandats
    participant STET as STET / ACH
    participant BD as Banque débiteur
    participant Deb as Débiteur

    Cred->>BPS: pain.008 demande de prélèvement
    BPS->>Mandat: Contrôle mandat
    Mandat-->>BPS: Mandat valide / invalide
    BPS->>STET: pacs.003
    STET->>BD: Présentation prélèvement
    BD->>Deb: Débit compte si accepté
    BD-->>STET: Acceptation / rejet / retour
    STET-->>BPS: pacs.002 / pacs.004
    BPS-->>Cred: Statut / reporting
```

### Points critiques

- mandat ;
- séquence de prélèvement ;
- R-transactions ;
- compte clôturé ;
- fonds insuffisants ;
- contestation ;
- réconciliation.

### Lecture GreenOps

Le SDD produit du carbone surtout via :

- retours ;
- litiges ;
- relances ;
- stockage mandat ;
- réconciliations ;
- conservation longue.

---

## 10. Flux BPCE type — Wero / SCT Inst

```mermaid
sequenceDiagram
    participant Client as Client BP/CE
    participant App as App Banque Populaire / Caisse d'Épargne
    participant Wero as Wero / EPI
    participant BPS as BPCE Payment Services
    participant Fraud as Fraude / AML
    participant TIPS as TIPS / Instant Payment
    participant BankB as Banque bénéficiaire

    Client->>App: Paiement Wero
    App->>Wero: Initiation paiement
    Wero->>BPS: Demande SCT Inst
    BPS->>Fraud: Contrôle fraude temps réel
    Fraud-->>BPS: Décision
    BPS->>BPS: Validation / idempotence
    BPS->>TIPS: Instruction instant payment
    TIPS->>BankB: Règlement instantané
    BankB-->>TIPS: Acceptation / rejet
    TIPS-->>BPS: Statut final
    BPS-->>Wero: Confirmation
    Wero-->>App: Résultat paiement
```

### Points critiques

- latence ;
- authentification ;
- fraude temps réel ;
- retry ;
- idempotence ;
- statut incertain ;
- disponibilité 24/7 ;
- expérience mobile.

### Lecture GreenOps

Le SCT Inst produit du carbone surtout via :

- infrastructure active en continu ;
- redondance ;
- retries ;
- timeouts ;
- monitoring permanent ;
- logs temps réel ;
- contrôles fraude.

---

## 11. Flux Natixis type — paiement corporate international

```mermaid
sequenceDiagram
    participant Corp as Client Corporate
    participant Nat as Natixis GTB / CIB
    participant AML as Conformité AML / Sanctions
    participant Swift as SWIFT
    participant Corr as Banque correspondante
    participant BenefBank as Banque bénéficiaire

    Corp->>Nat: Ordre paiement international
    Nat->>Nat: Validation format / convention client
    Nat->>AML: Screening AML / sanctions
    AML-->>Nat: OK / alerte
    Nat->>Swift: Message MT ou MX ISO 20022
    Swift->>Corr: Routage
    Corr->>BenefBank: Paiement vers bénéficiaire
    BenefBank-->>Nat: Statut / confirmation
```

### Points critiques

- formats clients ;
- conventions de remise ;
- devises ;
- banques correspondantes ;
- SWIFT ;
- sanctions ;
- faux positifs ;
- investigations ;
- statuts incomplets ;
- rapprochement cash management.

### Lecture GreenOps

Le cross-border produit du carbone surtout via :

- screening répété ;
- faux positifs ;
- traitements manuels ;
- stockage réglementaire ;
- mapping MT/MX ;
- logs détaillés ;
- investigations.

---

## 12. Flux Oney type — paiement fractionné

```mermaid
sequenceDiagram
    participant Client as Client final
    participant Merchant as Commerçant
    participant Oney as Oney
    participant Risk as Scoring / Risque
    participant Bank as Banque / carte / compte

    Client->>Merchant: Achat
    Merchant->>Oney: Demande paiement 3x/4x
    Oney->>Risk: Scoring / éligibilité
    Risk-->>Oney: Décision
    Oney-->>Merchant: Acceptation paiement
    Oney->>Bank: Paiement commerçant
    Oney->>Client: Échéancier
    Client-->>Oney: Remboursements successifs
```

### Points critiques

- scoring ;
- risque crédit ;
- parcours client ;
- autorisation carte ;
- prélèvements futurs ;
- relances ;
- réconciliation commerçant ;
- service client.

### Lecture GreenOps

Le paiement fractionné produit du carbone via :

- scoring ;
- appels référentiels ;
- parcours e-commerce ;
- échéanciers ;
- relances ;
- rejets de prélèvements ;
- notifications.

---

## 13. Flux API / PISP BPCE

Le HUB PISP de BPCE Payment Services permet un encaissement par initiation de paiement au moyen d’un SCT ou SCT Inst validé par le payeur dans son espace bancaire.

```mermaid
sequenceDiagram
    participant Merchant as Marchand / Créancier
    participant PISP as HUB PISP BPCE
    participant Bank as Banque du payeur
    participant Payeur as Payeur
    participant BPS as BPCE Payment Services
    participant Benef as Bénéficiaire

    Merchant->>PISP: Demande d'encaissement
    PISP->>Bank: Initiation SCT ou SCT Inst
    Bank->>Payeur: Authentification / consentement
    Payeur-->>Bank: Validation
    Bank->>BPS: Exécution paiement
    BPS->>Benef: Encaissement
    BPS-->>PISP: Statut
    PISP-->>Merchant: Confirmation
```

### Lecture architecture

Le PISP se situe entre :

- API ;
- DSP2 ;
- consentement client ;
- authentification forte ;
- SCT / SCT Inst ;
- paiement e-commerce ;
- reporting marchand.

### Lecture GreenOps

Le PISP peut réduire certains coûts liés à la carte, mais introduit :

- appels API ;
- authentification ;
- orchestration temps réel ;
- dépendance à la qualité des statuts ;
- besoin d’observabilité fine.

---

## 14. Flux Cash Management Natixis / Corporate

```mermaid
flowchart TD
    A[Paiement émis ou reçu] --> B[Core Banking]
    B --> C[Cash Management Engine]
    C --> D[camt.052 intraday]
    C --> E[camt.053 relevé]
    C --> F[camt.054 notification]
    D --> G[Trésorerie corporate]
    E --> H[ERP / Comptabilité]
    F --> I[Rapprochement automatique]
    I --> J{Match facture ?}
    J -- Oui --> K[Clôture automatique]
    J -- Non --> L[Exception comptable]
```

### Points critiques

- EndToEndId ;
- remittance information ;
- formats clients ;
- reporting intraday ;
- relevés complets ;
- ERP ;
- rapprochement ;
- archivage.

### Lecture GreenOps

Le cash management produit du carbone via :

- relevés volumineux ;
- duplication de données ;
- transformations client ;
- stockage ;
- logs ;
- exceptions de rapprochement.

---

## 15. Rôle d’ISO 20022 dans cet écosystème

ISO 20022 fournit le langage commun entre :

- initiation client ;
- interbancaire ;
- reporting ;
- retour ;
- cash management ;
- investigation ;
- conformité.

```mermaid
flowchart LR
    CLIENT[Client / Corporate] -->|pain| BANKA[Banque émettrice]
    BANKA -->|pacs| INFRA[STET / TIPS / SWIFT]
    INFRA -->|pacs| BANKB[Banque bénéficiaire]
    BANKB -->|camt| CLIENTB[Client / ERP]
    INFRA -->|pacs.002 / pacs.004| BANKA
    BANKA -->|pain.002 / camt| CLIENT
```

### Enjeux ISO 20022 par entité

| Entité | Enjeux ISO 20022 |
|---|---|
| Banque Populaire / Caisse d’Épargne | qualité données client, virements, notifications, Wero |
| BPCE Payment Services | industrialisation, transformation, routage, supervision |
| Natixis | corporate, cash management, cross-border, CBPR+ |
| Oney | données client, échéanciers, prélèvements associés |
| Wero / EPI | SCT Inst, temps réel, interopérabilité européenne |
| Estreem | standardisation processing carte, reporting, données transactionnelles |

---

## 16. Enjeux réglementaires

| Domaine | Règlement / cadre | Impact |
|---|---|---|
| Paiement instantané | Règlement Instant Payment | disponibilité SCT Inst, coûts, obligation d’accessibilité |
| Open Banking | DSP2 / DSP3 | API, consentement, SCA, PISP |
| Résilience | DORA | tests, incidents, tiers critiques, continuité |
| Durabilité | CSRD | reporting carbone, trajectoire RSE |
| Paiements internationaux | AML / sanctions | screening, conformité, investigations |
| Données | RGPD | données personnelles, conservation, sécurité |

---

## 17. Enjeux GreenOps spécifiques

| Domaine | Source de consommation | Leviers |
|---|---|---|
| SCT | batchs, rejets, logs | validation amont, compression, suppression replays |
| SDD | R-transactions, mandats, retours | qualité mandat, réduction retours, archivage froid |
| SCT Inst | retries, disponibilité 24/7 | idempotence, circuit breaker, maîtrise timeouts |
| Cross-border | AML, faux positifs, mapping | données structurées, screening efficace |
| Cash management | relevés volumineux | delta, compression, STP, réduction formats spécifiques |
| Oney | scoring, échéanciers, relances | automatisation, qualité data, réduction rejets |
| Wero | temps réel, API, mobile | optimisation latence, monitoring, statuts fiables |
| Carte / Estreem | autorisation, clearing, reporting | mutualisation, standardisation, observabilité |

---

## 18. Où se crée l’empreinte carbone

```mermaid
flowchart TD
    A[Acquisition ordre] --> B[Parsing / validation]
    B --> C[Mapping / transformation]
    C --> D[Appels référentiels]
    D --> E[AML / fraude / scoring]
    E --> F[Transmission infrastructure]
    F --> G[Retries / timeouts]
    G --> H[Statuts / retours]
    H --> I[Réconciliation]
    I --> J[Logs / traces]
    J --> K[Archivage]
    K --> L[Reporting]
```

### Principaux gaspillages

| Gaspillage | Exemple | Impact |
|---|---|---|
| Retry SCT Inst | timeout mal géré | CPU, réseau, latence |
| Rejet SDD | mandat invalide | retraitement, litige |
| Faux positif AML | donnée non structurée | investigation |
| Logs XML complets | message stocké plusieurs fois | stockage |
| Mapping multiple | legacy → MT → MX → interne | CPU |
| Batch relancé | fichier SCT rejeté | I/O, CPU |
| Reporting complet inutile | camt complet au lieu de delta | réseau, stockage |

---

## 19. KPI de pilotage

| KPI | Domaine | Objectif |
|---|---|---|
| nombre transactions / jour | métier | volumétrie |
| taux STP | métier / SI | automatisation |
| taux rejet SCT | qualité | réduire retraitements |
| taux R-transactions SDD | qualité / métier | réduire retours |
| taux timeout SCT Inst | SRE | réduire statuts incertains |
| taux retry | SRE / GreenOps | réduire gaspillage |
| P95/P99 latence | performance | maîtriser temps réel |
| taux faux positifs AML | conformité | réduire investigations |
| volume logs / transaction | GreenOps | réduire stockage |
| kWh / 1000 transactions | GreenOps | mesurer énergie |
| gCO2e / transaction | carbone | piloter SCI |
| coût / transaction | FinOps | piloter efficience |

---

## 20. Questions d’audit BPCE / Natixis

| Question | Objectif |
|---|---|
| Quels flux sont opérés par BPCE Payment Services ? | cartographier le socle groupe |
| Quels flux relèvent de Natixis GTB / CIB ? | isoler corporate / cross-border |
| Quelle part de volume revient à SCT, SDD, SCT Inst, carte ? | mesurer la volumétrie |
| Où sont faits les mappings MT / MX / ISO ? | réduire la complexité |
| Où sont les retries SCT Inst ? | réduire la surcharge |
| Quels sont les top motifs de rejet SCT / SDD ? | améliorer le STP |
| Quel est le taux de faux positifs AML ? | optimiser la conformité |
| Quels messages camt sont générés ? | maîtriser le cash management |
| Les logs stockent-ils le XML complet ? | réduire le stockage |
| Où mesurer gCO2e / transaction ? | piloter GreenOps |
| Quels tiers sont critiques DORA ? | piloter la résilience |
| Les infrastructures sont-elles observées de bout en bout ? | réduire les angles morts |

---

## 21. Architecture cible de référence

```mermaid
flowchart TD
    subgraph Canaux[Canaux]
        BPAPP[Apps Banque Populaire]
        CEAPP[Apps Caisse d'Épargne]
        WEROAPP[Wero]
        CORP[Corporate / Natixis GTB]
        MERCH[Commerçants / Oney / PISP]
        SWIFTIN[SWIFT / fichiers]
    end

    subgraph Integration[Couche intégration]
        APIGW[API Gateway]
        EAI[Middleware / EAI]
        MAP[Mapping canonique ISO 20022]
        IDEMP[Idempotence]
    end

    subgraph Controle[Contrôles]
        ISO[Validation ISO]
        AML[AML / sanctions]
        FRAUD[Fraude temps réel]
        RISK[Scoring / risque]
    end

    subgraph Processing[Traitements]
        SCT[SCT Engine]
        SDD[SDD Engine]
        INST[SCT Inst Engine]
        XB[Cross-border Engine]
        CASH[Cash Management]
        CARD[Carte / Estreem]
        BNPL[Oney / BNPL]
    end

    subgraph Infra[Infrastructures]
        STET[STET / ACH]
        TIPS[TIPS]
        T2[T2]
        SWIFT[SWIFT]
        CARDNET[Réseaux cartes / processing]
    end

    subgraph Obs[Observabilité / GreenOps]
        SLI[SLI / SLO]
        LOGS[Logs sobres]
        METRICS[Métriques]
        SCI[SCI / gCO2e transaction]
    end

    BPAPP --> APIGW
    CEAPP --> APIGW
    WEROAPP --> APIGW
    CORP --> EAI
    MERCH --> APIGW
    SWIFTIN --> EAI

    APIGW --> EAI
    EAI --> MAP
    MAP --> IDEMP
    IDEMP --> ISO
    ISO --> AML
    AML --> FRAUD
    FRAUD --> RISK

    RISK --> SCT
    RISK --> SDD
    RISK --> INST
    RISK --> XB
    RISK --> CASH
    RISK --> CARD
    RISK --> BNPL

    SCT --> STET
    SDD --> STET
    STET --> T2
    INST --> TIPS
    XB --> SWIFT
    CARD --> CARDNET

    SCT --> SLI
    SDD --> SLI
    INST --> SLI
    XB --> SLI
    CASH --> SLI
    CARD --> SLI
    BNPL --> SLI

    SLI --> METRICS
    LOGS --> SCI
    METRICS --> SCI
```

---

## 22. Lecture architecte

L’écosystème paiements BPCE / Natixis doit être lu comme un système distribué industriel.

Il combine :

```text
réseaux de distribution
+
payment factory
+
paiements SEPA
+
paiements instantanés
+
paiements internationaux
+
cash management
+
carte
+
paiement fractionné
+
API / Open Banking
+
conformité
+
observabilité
+
GreenOps
```

Le rôle de l’architecte est de réduire la complexité tout en maintenant la performance, la conformité et la résilience.

---

## 23. Synthèse

L’écosystème BPCE / Natixis est large, distribué, volumineux et critique.

Il couvre :

- les paiements de proximité Banque Populaire et Caisse d’Épargne ;
- le processing industriel via BPCE Payment Services ;
- les paiements corporate, internationaux et cash management via Natixis ;
- le paiement fractionné via Oney ;
- le paiement compte à compte avec Wero ;
- le processing carte avec Estreem ;
- les infrastructures STET, TIPS, T2 et SWIFT.

La cible d’architecture est une chaîne paiement :

- structurée ;
- industrialisée ;
- interopérable ;
- résiliente ;
- observable ;
- pilotée par les données ;
- optimisée en coût ;
- sobre en carbone.

---

## 24. Sources publiques consultées

- Groupe BPCE — Profil du groupe : https://www.groupebpce.com/le-groupe/profil/
- BPCE Digital & Payments — Données clés : https://www.digital-payments.groupebpce.com/donnees-cles/
- BPCE Digital & Payments : https://www.digital-payments.groupebpce.com/
- BPCE Payment Services / recrutement BPCE : https://recrutement.bpce.fr/
- Natixis — Payments : https://natixis.groupebpce.com/payments/
- API Store Groupe BPCE — Encaissement par initiation de paiement : https://apistore.groupebpce.com/fr/api/encaissement-par-initiation-de-paiement
- Newsroom Groupe BPCE — Wero e-commerce : https://newsroom.groupebpce.fr/
- Newsroom Groupe BPCE — acquisition Oney : https://newsroom.groupebpce.fr/
- STET — Instant Payments : https://www.stet.eu/en/solutions/our-services/instant-payments.html
- Banque centrale européenne — TIPS : https://www.ecb.europa.eu/paym/target/tips/
- Reuters — Estreem / BPCE / BNP Paribas : https://www.reuters.com/business/finance/bnp-paribas-bpce-join-forces-payment-processing-2025-02-13/
- Documents publics BPCE International / Océor : sources publiques historiques.
