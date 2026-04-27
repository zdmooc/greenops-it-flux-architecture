# 11 — Checklist d’audit ISO 20022

**Dépôt :** `greenops-it-flux-architecture`  
**Domaine :** ISO 20022 appliqué aux flux de paiements bancaires  
**Niveau :** Architecte solution senior / direction architecture / audit N3  
**Référence interne :** `ISO-11`

## Objectif du document

Fournir une checklist d’audit complète avec scoring 0 à 5, preuves attendues, questions et livrables pour évaluer une plateforme ISO 20022.

Ce document est écrit comme un livrable exploitable par une squad paiement, une équipe architecture, une production bancaire, une équipe SRE ou une mission de transformation type BPCE / Natixis. Il privilégie les décisions d’architecture, les impacts SI, les risques de production, les contrôles d’audit et les leviers GreenOps.

---


## 1. Barème de scoring

| Score | Niveau | Description |
|---:|---|---|
| 0 | Inexistant | Aucun dispositif identifié |
| 1 | Initial | Pratiques ad hoc, peu documentées |
| 2 | Répétable | Quelques standards, couverture partielle |
| 3 | Défini | Processus documenté et appliqué |
| 4 | Maîtrisé | Mesures, contrôles et automatisation |
| 5 | Optimisé | Amélioration continue, pilotage par KPI |

## 2. Checklist messages

| Contrôle | Question | Preuve | Score |
|---|---|---|---|
| Catalogue messages | Les messages supportés sont-ils listés ? | Catalogue pain/pacs/camt/remt | 0-5 |
| Versions | Les versions sont-elles gouvernées ? | Matrice versions/canaux | 0-5 |
| Statuts | Les statuts sont-ils normalisés ? | Table statut interne/ISO | 0-5 |
| Corrélation | Les identifiants sont-ils conservés ? | Logs/traces/requêtes | 0-5 |

## 3. Checklist mapping

| Contrôle | Question | Preuve | Score |
|---|---|---|---|
| Modèle canonique | Existe-t-il un modèle canonique ? | Schéma + ADR | 0-5 |
| Version mapping | Les règles sont-elles versionnées ? | Git/tag/release notes | 0-5 |
| Tests mapping | Les mappings sont-ils testés ? | Jeux de tests | 0-5 |
| Anti-point-à-point | Les mappings directs sont-ils maîtrisés ? | Cartographie flux | 0-5 |

## 4. Checklist validation

| Contrôle | Question | Preuve | Score |
|---|---|---|---|
| XML/XSD | Validation automatique ? | Pipeline, logs, tests | 0-5 |
| Market practice | SEPA/CBPR+ contrôlé ? | Règles/profils | 0-5 |
| Règles métier | Contrôles banque formalisés ? | Catalogue règles | 0-5 |
| Rejets | Rejets classifiés ? | Dashboard rejets | 0-5 |

## 5. Checklist performance

| Contrôle | Question | Preuve | Score |
|---|---|---|---|
| P95/P99 | Mesure par flux ? | Dashboard | 0-5 |
| Batch | Tests volumétrie ? | Rapports perf | 0-5 |
| Parser | DOM évité sur gros flux ? | Code/revue | 0-5 |
| Logs | Volume maîtrisé ? | Metrics logs | 0-5 |

## 6. Checklist production/SRE

| Contrôle | Question | Preuve | Score |
|---|---|---|---|
| Runbooks | Runbooks incidents ISO ? | Docs N2/N3 | 0-5 |
| Alerting | Alertes métier et technique ? | Règles alerting | 0-5 |
| Tracing | Trace distribuée ? | OpenTelemetry/logs | 0-5 |
| DLQ | Gestion rejets/reprises ? | Procédures + tests | 0-5 |

## 7. Checklist GreenOps

| Contrôle | Question | Preuve | Score |
|---|---|---|---|
| CPU/message | Mesuré ? | Metrics | 0-5 |
| gCO2e/transaction | Estimé ? | Méthode SCI | 0-5 |
| Rejets tardifs | Mesurés ? | Dashboard | 0-5 |
| Logs/message | Piloté ? | Metrics stockage | 0-5 |
| Backlog sobriété | Existant ? | Jira/roadmap | 0-5 |

## 8. Questions à poser

1. Quelles versions ISO sont supportées par canal ?
2. Quel est le taux de rejet par couche : XML, XSD, métier, infrastructure ?
3. Où est stockée la table de mapping des statuts ?
4. Comment retrouver un paiement avec `EndToEndId` ?
5. Combien de transformations subit une transaction SCT ?
6. Quel est le P99 SCT Inst ?
7. Quels payloads sont logués et pendant combien de temps ?
8. Les rejets tardifs sont-ils quantifiés ?
9. Existe-t-il un plan de décommissionnement des anciennes versions ?
10. Les runbooks ont-ils été testés en exercice de crise ?

## 9. Livrables d’audit

- cartographie flux ISO ;
- catalogue messages/versions ;
- matrice risques ;
- score de maturité ;
- backlog de remédiation priorisé ;
- architecture cible ;
- quick wins GreenOps ;
- plan 30/60/90 jours ;
- annexes preuves et extraits d’observabilité.

## 10. Exemple de synthèse scoring

| Domaine | Score | Commentaire |
|---|---:|---|
| Messages | 3 | Catalogue présent mais versions client incomplètes |
| Mapping | 2 | Trop de point-à-point |
| Validation | 3 | XSD OK, market practice partielle |
| Performance | 2 | P99 non suivi sur certains flux |
| SRE | 3 | Runbooks présents mais peu testés |
| GreenOps | 1 | Mesures carbone non industrialisées |
| Gouvernance | 2 | Décommissionnement non piloté |

---

## Synthèse architecte

Un programme ISO 20022 réussi ne se limite pas à changer des fichiers XML. Il impose une gouvernance de la donnée paiement, une stratégie de validation, un modèle canonique, une observabilité de bout en bout, une gestion stricte des versions et une mesure continue du coût opérationnel. Dans une banque de flux, les gains les plus importants viennent généralement de la réduction des rejets tardifs, de la diminution des mappings point-à-point, de la maîtrise des logs et de la capacité à diagnostiquer rapidement un paiement avec ses identifiants de corrélation.

## Points de vigilance récurrents

| Risque | Symptôme | Conséquence | Mesure de prévention |
|---|---|---|---|
| Confusion syntaxe / sémantique | XML valide mais paiement rejeté | Incident métier | Règles métier et market practice en plus du XSD |
| Mapping point-à-point | Multiplication des transformations | Coût, dette, erreurs | Modèle canonique gouverné |
| Validation tardive | Rejet après plusieurs étapes | Retraitements, carbone inutile | Validation amont et contrats d’interface |
| Version mal maîtrisée | Clients ou infrastructures désalignés | Rejets massifs | Catalogue de versions et tests de non-régression |
| Observabilité insuffisante | Paiement introuvable | MTTR élevé | MessageId, EndToEndId, TxId, correlationId partout |
| Logs excessifs | Volumes énormes | Coût stockage et empreinte carbone | Logs structurés, sampling, rétention adaptée |


## Annexe — métriques minimales recommandées

| Métrique | Label minimal | Utilisation |
|---|---|---|
| `payment_messages_total` | flux, message_type, version, channel | Volumétrie métier |
| `payment_rejections_total` | flux, rejection_stage, reason_code | Qualité et incidents |
| `payment_processing_duration_seconds` | flux, step, percentile | Performance SRE |
| `payment_payload_size_bytes` | message_type, version | GreenOps et capacité |
| `payment_retry_total` | service, reason | Résilience et gaspillage |
| `payment_log_bytes_total` | service, flux | Coût logs |

## Annexe — questions de revue d’architecture

- La solution distingue-t-elle clairement le format externe et le modèle interne ?
- Les règles de validation sont-elles traçables, versionnées et testées ?
- Les identifiants de corrélation sont-ils propagés sans rupture ?
- Le traitement peut-il être diagnostiqué sans lire le payload complet ?
- Les anciennes versions ont-elles une date de fin de vie ?
- Les flux batch et temps réel sont-ils séparés dans l’architecture et les SLO ?
- Les métriques GreenOps permettent-elles de prioriser des actions concrètes ?
- Les runbooks sont-ils testés et reliés aux alertes ?
