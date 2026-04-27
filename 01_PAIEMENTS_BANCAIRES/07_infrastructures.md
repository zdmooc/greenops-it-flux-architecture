# 07 — Infrastructures de Paiement : STET, TIPS, T2, SWIFT

## 1. Objectif du document

Ce document présente les principales infrastructures utilisées dans les flux de paiements bancaires.

Il couvre :

- STET / ACH ;
- TIPS ;
- T2 / TARGET ;
- SWIFT ;
- le rôle de chaque infrastructure ;
- les différences entre compensation, règlement et messagerie ;
- les impacts architecture ;
- les impacts GreenOps.

---

# 2. Vue globale

Une infrastructure de paiement permet aux banques d’échanger, compenser, régler ou transmettre des instructions de paiement.

Toutes les infrastructures ne font pas la même chose.

```text
Messagerie ≠ Compensation ≠ Règlement