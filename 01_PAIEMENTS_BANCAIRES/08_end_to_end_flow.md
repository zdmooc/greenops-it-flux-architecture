# 08 — Vue End-to-End des Flux de Paiements Bancaires

## 1. Objectif du document

Ce document consolide les flux SCT, SDD, SCT Inst, cross-border et cash management dans une vue end-to-end.

Il permet de comprendre :

- comment les différents flux s’articulent ;
- où intervient ISO 20022 ;
- où se situent les infrastructures ;
- où apparaissent les erreurs, rejets et retries ;
- où se crée la consommation IT ;
- comment piloter une architecture paiement avec une vision GreenOps.

---

# 2. Vue d’ensemble

Une plateforme de paiement complète doit gérer plusieurs types de flux :

| Flux | Nature | Mode | Infrastructure principale |
|---|---|---|---|
| SCT | Virement SEPA classique | batch / différé | STET / ACH |
| SDD | Prélèvement SEPA | batch / mandat | STET / ACH |
| SCT Inst | Virement instantané | temps réel | TIPS |
| Cross-border | Paiement international | interbancaire | SWIFT |
| Cash Management | Reporting / relevés | batch ou temps réel | camt / ERP / API |

---

# 3. Schéma global end-to-end

```mermaid
flowchart LR
    CLIENT[Client / Corporate] --> CHANNEL[Canaux<br/>Mobile, Web, API, EBICS, MFT]
    CHANNEL --> HUB[Payment Hub]

    HUB --> VALID[Validation<br/>ISO 20022, métier, conformité]
    VALID --> ROUTING[Routage paiement]

    ROUTING --> SCT[SCT]
    ROUTING --> SDD[SDD]
    ROUTING --> INST[SCT Inst]
    ROUTING --> XB[Cross-border]

    SCT --> STET[STET / ACH]
    SDD --> STET
    INST --> TIPS[TIPS]
    XB --> SWIFT[SWIFT]

    STET --> T2[T2 / Règlement final]
    TIPS --> BANKB[Banque bénéficiaire]
    SWIFT --> CORR[Banques correspondantes]

    T2 --> BANKB
    CORR --> BANKB

    BANKB --> CORE[Core Banking]
    CORE --> REPORT[Cash Management<br/>camt.052 / camt.053 / camt.054]
    REPORT --> ERP[ERP / Trésorerie client]

    HUB --> OBS[Observabilité<br/>SLI/SLO, logs, traces]
    OBS --> GREEN[GreenOps<br/>SCI, gCO2e/transaction]