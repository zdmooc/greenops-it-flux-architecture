# 01 — Fondamentaux GreenOps appliqués aux flux de paiements

## 1. Pourquoi GreenOps devient critique dans les paiements

Les systèmes de paiements bancaires (SCT, SDD, SCT Inst, SWIFT, TIPS) traitent des volumes massifs en continu.
Historiquement optimisés pour la disponibilité et la conformité, ils ne l’étaient pas pour la sobriété énergétique.

Aujourd’hui, avec CSRD, REEN et DORA, l’empreinte carbone devient un enjeu stratégique.

---

## 2. Définition du GreenOps

GreenOps = discipline visant à mesurer, piloter et réduire l’empreinte carbone IT.

1 transaction = 1 consommation énergétique = 1 empreinte carbone

Objectif :
Mesurer → Comprendre → Optimiser → Piloter

---

## 3. Chaîne de traitement ISO 20022

Message → Parsing XML → Validation → Mapping → Enrichissement → AML → Routing → Clearing → Statuts → Logs → Stockage

Chaque étape consomme CPU, mémoire et stockage.

---

## 4. Paradoxe ISO 20022

ISO 20022 est plus lourd (XML) mais réduit les erreurs.

Le vrai coût n’est pas le XML mais les erreurs et retraitements.

---

## 5. Exemple SCT batch

5 000 000 transactions, 1% erreur = 50 000 retraitements.

Impact :
CPU doublé, logs doublés, stockage doublé.

---

## 6. Exemple SCT Inst

1 000 000 transactions, 1% timeout, retry ×2 = 20 000 traitements inutiles.

---

## 7. Sources de gaspillage

- retry
- logs XML complets
- mapping multiple
- validation tardive
- données inutiles

---

## 8. Principe clé

Le problème n’est pas le volume mais le gaspillage.

---

## 9. Axes d’optimisation

- validation amont
- idempotence
- logs sobres
- modèle canonique
- purge stockage

---

## 10. KPI

- gCO2e / transaction
- CPU / message
- retry rate
- reject rate
- taille XML

---

## 11. Conclusion

ISO 20022 devient un levier GreenOps s’il est bien architecturé.
