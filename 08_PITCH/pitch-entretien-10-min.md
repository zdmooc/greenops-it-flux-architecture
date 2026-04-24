# Pitch entretien — 10 minutes

## 0:00–1:00 — Introduction

Je positionne le sujet de décarbonation IT Flux non pas comme un simple chantier RSE, mais comme un sujet d’architecture et d’optimisation d’un système critique de paiement.

Le périmètre combine paiements SCT, SCT Inst, SDD, batchs, contrôles, observabilité et CI/CD. Les contraintes sont fortes : SLA, disponibilité, DORA, sécurité, volumétrie, dette legacy et objectifs carbone.

## 1:00–2:30 — Ma lecture du besoin

Le besoin réel est double :

1. réduire les émissions des 5 applications les plus émettrices : -6 % fin 2026, -20 % horizon 2030 ;
2. industrialiser SonarQube et Checkmarx pour réduire dette technique, vulnérabilités et non-qualité.

Ma conviction : les deux sujets sont liés. Une application instable, mal observée, avec trop de retries, trop de logs ou trop de dette technique consomme plus.

## 2:30–4:00 — Méthode

Je propose une démarche en 6 étapes :

1. établir la baseline ;
2. cartographier les flux et environnements ;
3. mesurer consommation, volumétrie, retries, logs, CPU/RAM/stockage ;
4. prioriser les actions ;
5. exécuter par vagues ;
6. mesurer les gains avant/après.

## 4:00–6:00 — Modèles d’optimisation

Le différenciateur est l’usage de modèles mathématiques et de recherche opérationnelle.

- SCI pour mesurer l’intensité carbone par transaction ;
- files d’attente pour dimensionner SCT Inst et API critiques ;
- PLNE pour le right-sizing et l’extinction non-prod ;
- scheduling pour les batchs ;
- knapsack pour choisir les quick wins sous budget limité ;
- multi-objectifs pour arbitrer carbone, coût, SLA et risque.

## 6:00–8:00 — Architecture cible

L’architecture cible repose sur :

- observabilité unifiée Ops/SRE/GreenOps ;
- policies de logs, retries, timeouts ;
- right-sizing piloté par les métriques ;
- réduction du polling et événementialisation progressive ;
- CI/CD standardisé avec SonarQube et Checkmarx ;
- reporting exécutif mensuel.

## 8:00–9:30 — Roadmap

Court terme 2026 : quick wins.

- extinction non-prod ;
- right-sizing ;
- réduction logs ;
- réduction retries ;
- premiers quality gates.

Moyen terme 2027–2030 : transformation.

- optimisation SQL ;
- batch scheduling ;
- event-driven architecture ;
- rationalisation données ;
- gouvernance continue.

## 9:30–10:00 — Conclusion

Ma valeur ajoutée est de relier architecture, run, DevSecOps, GreenOps et modèles d’optimisation pour produire une trajectoire réaliste et pilotable.

Phrase finale :

> Je ne cherche pas seulement à mesurer le carbone. Je cherche à rendre le système de paiement plus efficient, plus stable, plus sobre et mieux gouverné, sans compromettre les SLA critiques.
