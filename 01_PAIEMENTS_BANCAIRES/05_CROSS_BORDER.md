# 05 — Paiements Transfrontaliers : Cross-Border Payments & SWIFT

## 1. Objectif du document

Ce document présente les paiements transfrontaliers, c’est-à-dire les paiements envoyés entre banques situées dans des pays, devises ou zones de compensation différentes.

Il couvre :

- la définition métier du paiement cross-border ;
- les acteurs impliqués ;
- le rôle de SWIFT ;
- la différence entre MT et ISO 20022 MX ;
- le processus end-to-end ;
- les contraintes conformité, sanctions, AML ;
- les impacts SI ;
- les impacts GreenOps ;
- les leviers d’optimisation architecture.

---

# 2. Définition

Un paiement transfrontalier est un paiement envoyé d’un pays vers un autre, souvent avec :

- une devise différente ;
- une banque correspondante ;
- plusieurs intermédiaires ;
- des contrôles de conformité renforcés ;
- des délais plus longs qu’un paiement domestique ;
- des frais potentiellement plus élevés.

Exemples :

- entreprise française qui paie un fournisseur américain ;
- banque européenne qui envoie des USD ;
- paiement corporate multi-devises ;
- règlement international entre institutions financières ;
- paiement hors zone SEPA.

---

# 3. Vue simple

```text
Client donneur d’ordre
        ↓
Banque émettrice
        ↓
SWIFT / réseau bancaire international
        ↓
Banque correspondante éventuelle
        ↓
Banque bénéficiaire
        ↓
Client bénéficiaire