# 07 — Performance ISO 20022

**Dépôt :** `greenops-it-flux-architecture`  
**Domaine :** ISO 20022 appliqué aux flux de paiements bancaires  
**Niveau :** Architecte solution senior / direction architecture / audit N3  
**Référence interne :** `ISO-07`

## Objectif du document

Analyser et optimiser les coûts CPU, mémoire, I/O, latence, logs et stockage des traitements ISO 20022 pour les batchs SCT/SDD et le temps réel SCT Inst.

Ce document est écrit comme un livrable exploitable par une squad paiement, une équipe architecture, une production bancaire, une équipe SRE ou une mission de transformation type BPCE / Natixis. Il privilégie les décisions d’architecture, les impacts SI, les risques de production, les contrôles d’audit et les leviers GreenOps.

---


## 1. Pourquoi ISO 20022 peut coûter cher

XML est verbeux. Les messages ISO 20022 peuvent contenir de nombreux éléments, namespaces, informations de parties, remittance, statuts et données de conformité. Le coût vient de la combinaison : parsing, validation XSD, transformation, enrichissement, stockage, logs, sérialisation, désérialisation et retries.

## 2. DOM vs SAX/StAX

| Parser | Principe | Avantage | Risque |
|---|---|---|---|
| DOM | Charge tout le document en mémoire | Simple à manipuler | Mémoire élevée |
| SAX | Lecture événementielle | Très faible mémoire | Code plus complexe |
| StAX | Streaming pull parser | Bon compromis | Nécessite discipline |

Pour les gros fichiers SCT/SDD, DOM peut provoquer des pics mémoire importants. Pour les traitements batch volumineux, un parser streaming est généralement préférable.

## 3. Validation XSD coûteuse

La validation XSD est nécessaire mais peut coûter cher si elle est répétée plusieurs fois. Recommandations :

- compiler/cache des schémas ;
- éviter de revalider le même payload à chaque étape ;
- distinguer validation canal et validation interne ;
- mesurer le coût moyen par message ;
- paralléliser avec contrôle de back-pressure.

## 4. Batch SCT/SDD

Les batchs volumineux ont des contraintes différentes du temps réel : débit, mémoire, reprise sur erreur, découpage, checkpoints, stockage temporaire.

```mermaid
flowchart LR
    A[Fichier pain.001/pain.008] --> B[Découpage lots]
    B --> C[Validation streaming]
    C --> D[Mapping canonique]
    D --> E[Persist checkpoint]
    E --> F[Emission pacs]
    F --> G[Statuts pain.002/camt]
```

## 5. SCT Inst temps réel

SCT Inst impose une latence très faible et une réponse rapide. Les optimisations portent sur :

- validation minimale bloquante ;
- caches référentiels chauds ;
- appels conformité optimisés ;
- timeouts stricts ;
- circuit breakers ;
- logs sobres ;
- éviter transformations inutiles ;
- priorité aux chemins critiques.

## 6. Latence P95/P99

| KPI | Sens | Usage |
|---|---|---|
| P50 | Médiane | Vue générale |
| P95 | 95 % sous ce seuil | SLA standard |
| P99 | 99 % sous ce seuil | Détection queues/lenteurs |
| P99.9 | Extrêmes | Flux critiques instant payment |

## 7. Exemples chiffrés indicatifs

| Scénario | Volume | Risque | Optimisation |
|---|---:|---|---|
| Fichier SCT 100k transactions | 100 000 tx | Mémoire DOM | Streaming + découpage |
| camt.053 fin de journée | 1 fichier lourd | I/O et stockage | Compression + pagination |
| SCT Inst API | 1 tx | Latence P99 | Cache + validation ciblée |
| Retours pacs.002 massifs | 50k statuts | Corrélation coûteuse | Index sur ids |

## 8. Mémoire et CPU

Points à surveiller :

- taille moyenne message ;
- taille maximale payload ;
- allocation objets XML ;
- garbage collection ;
- nombre de transformations ;
- validation répétée ;
- sérialisation JSON/XML ;
- chiffrement/déchiffrement ;
- compression.

## 9. Logs et stockage

Les logs peuvent dépasser le coût du traitement lui-même si les payloads complets sont journalisés. Règles :

- jamais de données sensibles complètes en logs ;
- loguer les identifiants, statuts, erreurs, durées, tailles ;
- masquer IBAN, noms, adresses si nécessaire ;
- utiliser sampling sur succès ;
- conserver les payloads dans un coffre/audit si besoin, pas dans les logs applicatifs ;
- définir des rétentions par usage.

## 10. Compression

La compression réduit le stockage et les transferts mais consomme du CPU. Elle est pertinente pour archives, camt volumineux, échanges batch, mais moins pour les chemins SCT Inst temps réel.

## 11. Optimisation GreenOps

| Levier | Gain technique | Gain carbone |
|---|---|---|
| Streaming parser | Moins mémoire | Moins CPU/GC |
| Validation unique | Moins traitement | Moins énergie/message |
| Réduction retries | Moins charge | Moins gCO2e/transaction |
| Logs sobres | Moins stockage | Moins énergie stockage |
| Rejet amont | Moins retraitement | Moins CPU gaspillé |
| Back-pressure | Moins saturation | Moins incidents |

## 12. Checklist performance

- Les schémas XSD sont-ils compilés/cache ?
- Les fichiers batch sont-ils découpés ?
- Les parsers streaming sont-ils utilisés pour gros volumes ?
- Les index existent-ils sur `MessageId`, `EndToEndId`, `TxId` ?
- Les logs contiennent-ils des payloads complets ?
- Les métriques P95/P99 existent-elles par flux ?
- Les retries sont-ils bornés ?
- Les rejets tardifs sont-ils mesurés ?

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
