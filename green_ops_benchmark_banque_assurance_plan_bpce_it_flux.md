# GreenOps Benchmark Banque & Assurance — Version détaillée expert

---

# 1. Objectif

Ce document est un **référentiel d’analyse complet** permettant :

- de comprendre **comment les banques et assurances réduisent leur empreinte carbone**
- d’identifier les **mécanismes concrets utilisés**
- de construire une **stratégie GreenOps industrialisée pour BPCE IT Flux**

---

# 2. Concepts fondamentaux (expliqués simplement)

## 2.1 Intensité carbone applicative

👉 Concept : mesurer l’impact carbone d’une application par unité utile.

Formule :
- gCO2e / transaction
- gCO2e / batch
- gCO2e / API call

👉 Explication :
Deux applications peuvent consommer autant d’énergie, mais celle qui traite plus de transactions est **plus efficace écologiquement**.

---

## 2.2 Modèle SCI (Software Carbon Intensity)

SCI = (E × I + M) / R

👉 Explication :
- E = énergie consommée
- I = intensité carbone de l’électricité
- M = impact matériel (serveurs)
- R = service rendu

👉 Lecture simple :
> combien de carbone pour produire une unité métier

---

## 2.3 GreenOps

👉 Concept : appliquer les principes FinOps au carbone.

👉 Explication :
On ne pilote plus seulement :
- le coût
- la performance

Mais aussi :
- le carbone

---

# 3. Benchmark détaillé banques & assurances

## 3.1 BNP Paribas

### Données clés
- -54 % émissions opérationnelles depuis 2019
- objectif neutralité carbone long terme

### Leviers utilisés
- optimisation immobilière
- réduction déplacements
- data centers optimisés

👉 Explication :
BNP agit d’abord sur **les gros postes visibles** avant d’aller sur l’IT.

👉 Leçon BPCE :
Commencer par **mesure simple + KPI direction**.

---

## 3.2 Crédit Agricole (CA-GIP)

### Données clés
- mesure carbone par produit IT

### Leviers
- catalogue IT
- responsabilisation équipes

👉 Explication :
Chaque service IT a une fiche avec :
- coût
- carbone
- usage

👉 Leçon BPCE :
Créer un **catalogue IT Flux carbone-aware**.

---

## 3.3 Natixis

### Données clés
- Green Weighting Factor

👉 Explication :
Chaque projet est noté selon son impact environnemental.

👉 Leçon BPCE :
Créer un **score applicatif multi-critères**.

---

## 3.4 Société Générale

### Données clés
- -36 % atteint en 2024 vs 2019
- objectif -50 % en 2030

👉 Explication :
Trajectoire progressive avec jalons.

👉 Leçon BPCE :
Fixer des **objectifs intermédiaires mesurables**.

---

## 3.5 Banque Postale

### Leviers
- écoconception
- réduction data

👉 Explication :
Moins de données = moins de stockage = moins de carbone.

👉 Leçon BPCE :
Optimiser :
- logs
- bases
- API

---

## 3.6 Allianz

### Leviers
- efficacité énergétique IT

👉 Explication :
Optimiser l’infrastructure a un impact direct.

---

# 4. Trajectoire BPCE / Natixis (modélisée)

## 4.1 Hypothèse réaliste

| Année | Indice carbone (base 100 en 2019) |
|------|----------------------------------|
| 2019 | 100 |
| 2020 | 95 |
| 2021 | 90 |
| 2022 | 88 |
| 2023 | 85 |
| 2024 | 85 (-15%) |
| 2025 | 82 |
| 2026 | 79 (-6%) |
| 2027 | 75 |
| 2028 | 72 |
| 2029 | 70 |
| 2030 | 68 (-20%) |

👉 Explication :
- phase 1 : gains faciles (infra, énergie)
- phase 2 : optimisation IT
- phase 3 : transformation profonde

---

# 5. Leviers détaillés BPCE IT Flux

Cette section transforme le benchmark banques/assurances en **plan d’action concret pour BPCE IT Flux**. L’objectif n’est pas seulement de dire « il faut réduire le carbone », mais de montrer **sur quoi agir**, **comment mesurer**, **comment prioriser**, et **comment démontrer les gains**.

---

## 5.1 Tableau de synthèse des leviers réutilisables par BPCE IT Flux

| Levier | Inspiration marché | Application BPCE IT Flux | Gain attendu |
|---|---|---|---|
| **Baseline carbone applicative** | CA-GIP mesure l’empreinte à la maille des produits IT. | Mesurer chaque application : infrastructure, CPU, mémoire, stockage, réseau, batchs, logs, dépendances. | Identifier les 5 applications les plus émettrices. |
| **Intensité carbone par transaction** | Le modèle SCI mesure le carbone par unité fonctionnelle. | gCO2e / virement, gCO2e / prélèvement, gCO2e / batch, gCO2e / 1000 appels API. | Comparer les applications malgré des volumes différents. |
| **Green Weighting Factor IT** | Natixis utilise une logique bonus-malus climat. | Score application = carbone + coût + criticité + dette technique + risque. | Prioriser objectivement les chantiers. |
| **Budget carbone IT** | La Poste utilise une logique de budget carbone pour piloter sa trajectoire. | Budget carbone annuel par domaine : SCT, SDD, instant payment, fraude, reporting. | Empêcher la dérive carbone des nouveaux projets. |
| **GreenOps + FinOps** | La FinOps Foundation relie optimisation cloud, coût et durabilité. | Mutualiser coût cloud/on-premise + carbone + capacité. | Réduire gaspillage infrastructure et coûts. |
| **Right-sizing infrastructure** | Pratique standard Green IT / GreenOps. | Ajuster CPU/mémoire, réduire surprovisionnement, supprimer environnements dormants. | Quick wins rapides. |
| **Optimisation batch** | Très applicable aux flux bancaires. | Décaler batchs non critiques, grouper traitements, éviter retries massifs. | Moins de pics CPU et meilleure efficacité. |
| **Réduction logs / données** | Le numérique responsable cible stockage, données et data centers. | Politique logs : niveau, durée, compression, archivage, suppression. | Gain stockage + I/O + coût. |
| **CI/CD responsable** | Croisement DevSecOps + GreenOps. | Quality gate carbone dans Jenkins/GitHub Actions : taille image, vulnérabilités, duplication, complexité, dépendances. | Empêcher la dette carbone dès la livraison. |
| **Écoconception logicielle** | La Banque Postale met en avant la performance numérique responsable. | Revue API, pagination, cache, réduction appels inutiles, requêtes SQL optimisées. | Baisse CPU / base de données / réseau. |
| **Formation des squads** | Banque de France : sensibilisation massive aux enjeux climatiques. | Former squads IT Flux + production + architecture + infogéreur. | Changement durable des pratiques. |
| **Reporting direction** | BNP, SG, BPCE publient des trajectoires chiffrées. | Dashboard mensuel : baseline, gains, risque, avancement -6 % / -20 %. | Pilotage lisible pour DSI / métiers. |

---

## 5.2 Baseline carbone applicative

### Définition

La baseline carbone applicative est le **point de départ mesuré**. Elle permet de savoir combien une application consomme et émet avant toute optimisation.

Sans baseline, il est impossible de prouver une réduction de -6 % ou -20 %.

### Ce qu’il faut mesurer

Pour chaque application IT Flux :

| Dimension | Mesure attendue | Exemple |
|---|---|---|
| CPU | consommation CPU moyenne et pic | 450 vCPU-heures / mois |
| Mémoire | mémoire réservée et réellement utilisée | 1,2 To-heures / mois |
| Stockage | volumétrie données + logs | 8 To actifs + 20 To archives |
| Réseau | trafic entrant/sortant | 12 To / mois |
| Batch | durée, fréquence, ressources consommées | batch EOD de 2h30 |
| API | nombre d’appels et coût moyen | 250 millions appels / mois |
| Logs | volume journalier et rétention | 500 Go / jour, rétention 90 jours |

### Application BPCE

Pour IT Flux, la baseline doit être construite par domaine :

- SCT : virements SEPA classiques
- SCT Inst : virements instantanés
- SDD : prélèvements
- fraude : contrôles et scoring
- reporting : réglementaire, métier, supervision
- batch EOD : traitements de fin de journée

### KPI de pilotage

| KPI | Usage |
|---|---|
| tCO2e / application / an | comparer les applications |
| gCO2e / transaction | comparer les flux |
| kgCO2e / batch | suivre les traitements lourds |
| gCO2e / 1000 appels API | mesurer les APIs |
| tCO2e / environnement | comparer dev, recette, préprod, prod |

### Gain attendu

Le premier gain n’est pas immédiatement une réduction. Le premier gain est la **visibilité**. On identifie les cinq applications qui justifient le plus d’effort.

---

## 5.3 Intensité carbone par transaction

### Définition

L’intensité carbone par transaction mesure le carbone émis pour produire une unité métier utile.

Exemples :

- un virement traité
- un prélèvement exécuté
- un contrôle fraude réalisé
- un batch terminé
- 1000 appels API servis

### Pourquoi c’est important

Une application avec de fortes émissions totales n’est pas forcément mauvaise si elle traite énormément de transactions. À l’inverse, une application peu utilisée mais très consommatrice peut être inefficace.

### Application BPCE

| Flux | Unité fonctionnelle recommandée |
|---|---|
| SCT | gCO2e / virement SEPA |
| SCT Inst | gCO2e / virement instantané |
| SDD | gCO2e / prélèvement |
| API fraude | gCO2e / 1000 appels API |
| Batch EOD | kgCO2e / exécution batch |
| Reporting | kgCO2e / rapport produit |

### Exemple de lecture

Si l’application A émet 10 tCO2e/an pour 100 millions de transactions, et l’application B émet 5 tCO2e/an pour 5 millions de transactions, alors B est beaucoup moins efficace malgré une émission totale plus faible.

### Gain attendu

Ce levier permet de comparer les applications de manière juste et d’éviter les mauvais arbitrages.

---

## 5.4 Green Weighting Factor IT

### Définition

Le Green Weighting Factor IT est un score de priorisation qui combine plusieurs dimensions : carbone, coût, criticité, dette technique, risque opérationnel et complexité de transformation.

### Inspiration

Natixis a utilisé une logique de bonus-malus climat pour orienter ses choix financiers. BPCE peut reprendre le principe, mais l’appliquer aux systèmes IT.

### Formule possible

Score GreenOps =

- 30 % carbone
- 20 % coût
- 20 % criticité métier
- 15 % dette technique
- 10 % risque opérationnel
- 5 % facilité de mise en œuvre

### Application BPCE

| Application | Carbone | Coût | Criticité | Dette | Risque | Score total |
|---|---:|---:|---:|---:|---:|---:|
| SCT Core | 5 | 5 | 5 | 4 | 5 | Très prioritaire |
| SDD Batch | 4 | 4 | 4 | 3 | 3 | Prioritaire |
| Reporting | 3 | 3 | 2 | 4 | 2 | Moyen |
| Environnement recette | 4 | 5 | 1 | 2 | 1 | Quick win |

### Gain attendu

Ce levier permet de sortir du débat subjectif. On ne choisit pas les chantiers au ressenti, mais selon une grille explicite.

---

## 5.5 Budget carbone IT

### Définition

Un budget carbone IT fixe une enveloppe annuelle d’émissions à ne pas dépasser, exactement comme un budget financier.

### Application BPCE

Chaque domaine reçoit une trajectoire :

| Domaine | Budget carbone annuel | Objectif |
|---|---:|---|
| SCT | baisse progressive | réduire coût par virement |
| SCT Inst | stabilisation malgré hausse volume | éviter explosion carbone |
| SDD | réduction batchs | optimiser traitements groupés |
| Fraude | maîtrise IA/API | limiter appels inutiles |
| Reporting | réduction stockage et recalculs | éviter duplications |

### Pourquoi c’est utile

Sans budget carbone, les nouveaux projets peuvent annuler les gains obtenus ailleurs.

### Gain attendu

Le budget carbone évite l’effet rebond : on optimise une application, mais une autre consomme davantage ensuite.

---

## 5.6 GreenOps + FinOps

### Définition

FinOps pilote les coûts IT. GreenOps ajoute la dimension carbone. Les deux doivent fonctionner ensemble.

### Application BPCE

Un même dashboard doit montrer :

- coût mensuel
- consommation CPU/mémoire
- émissions estimées
- taux d’utilisation réel
- gaspillage détecté

### Exemple

Une machine ou un namespace peut coûter cher, consommer beaucoup, mais être utilisé seulement 15 % du temps. C’est un candidat prioritaire.

### Gain attendu

Réduction simultanée :

- du coût
- du carbone
- du gaspillage infrastructure

---

## 5.7 Right-sizing infrastructure

### Définition

Le right-sizing consiste à aligner les ressources réservées avec les ressources réellement utilisées.

### Application BPCE

Actions possibles :

- réduire CPU requests trop élevés
- réduire mémoire réservée non utilisée
- arrêter environnements hors horaires ouvrés
- supprimer VM ou pods obsolètes
- mutualiser environnements de test

### Exemple

Un environnement de recette allumé 24h/24 alors qu’il est utilisé 8h/jour génère une consommation inutile.

### Gain attendu

C’est souvent un quick win, car il ne nécessite pas forcément de refonte applicative.

---

## 5.8 Optimisation batch

### Définition

Un batch est un traitement automatisé exécuté à un moment donné. Dans les systèmes bancaires, les batchs peuvent consommer énormément de ressources sur des fenêtres courtes.

### Application BPCE

Actions :

- identifier les batchs les plus longs
- mesurer CPU/mémoire par batch
- réduire les retries automatiques
- supprimer les recalculs inutiles
- paralléliser intelligemment
- lisser la charge hors pics métier
- décaler les batchs non critiques sur des périodes plus favorables

### Exemple IT Flux

Un batch SDD qui relit toute une table chaque nuit peut être remplacé par une logique incrémentale ne traitant que les nouvelles opérations.

### Gain attendu

Réduction des pics CPU, amélioration SLA, baisse consommation énergétique.

---

## 5.9 Réduction logs et données

### Définition

Les logs, traces, exports et données dupliquées consomment du stockage, de l’I/O, du réseau et du temps de traitement.

### Application BPCE

Actions :

- réduire logs DEBUG en production
- définir une rétention par criticité
- compresser les archives
- supprimer exports redondants
- limiter les duplications entre outils
- archiver en stockage froid
- éviter les payloads trop verbeux dans les traces

### Exemple

Un service qui produit 500 Go de logs par jour avec 90 jours de rétention génère 45 To de stockage logique, sans compter réplication et sauvegarde.

### Gain attendu

Réduction stockage, I/O, coût observabilité, temps de recherche et empreinte carbone.

---

## 5.10 CI/CD responsable

### Définition

Le CI/CD responsable intègre des contrôles GreenOps dans les pipelines de livraison.

### Application BPCE

Quality gates possibles :

- taille image Docker maximale
- seuil de duplication de code
- complexité cyclomatique
- dépendances inutilisées
- vulnérabilités bloquantes
- tests trop longs ou redondants
- consommation approximative du build

### Exemple pipeline

Un build qui reconstruit tout à chaque commit alors que seuls deux modules changent consomme inutilement du temps CPU.

### Gain attendu

Réduction de la dette carbone dès la livraison logicielle.

---

## 5.11 Écoconception logicielle

### Définition

L’écoconception logicielle vise à construire des applications plus sobres dès la conception.

### Application BPCE

Actions :

- APIs paginées
- caches maîtrisés
- réduction appels interservices
- requêtes SQL optimisées
- suppression traitements inutiles
- limitation payload JSON/XML
- architecture événementielle quand utile
- découplage des traitements non temps réel

### Exemple

Une API qui retourne 500 champs alors que l’écran n’en utilise que 20 consomme inutilement réseau, CPU et mémoire.

### Gain attendu

Baisse durable CPU, base de données, réseau et latence.

---

## 5.12 Formation des squads

### Définition

Une démarche GreenOps ne fonctionne pas seulement avec des outils. Elle exige que les équipes comprennent comment leurs décisions techniques créent ou réduisent du carbone.

### Public cible BPCE

- Product Owners
- Tech Leads
- développeurs
- architectes
- équipes production
- SRE
- DevSecOps
- infogéreur

### Contenu de formation

- lecture des KPI carbone
- bonnes pratiques logs
- bonnes pratiques batch
- optimisation API
- FinOps + GreenOps
- qualité code et dette carbone

### Gain attendu

Changement durable des comportements et meilleure appropriation par les équipes.

---

## 5.13 Reporting direction

### Définition

Le reporting direction transforme les métriques techniques en informations lisibles pour les décideurs.

### Application BPCE

Dashboard mensuel :

| Indicateur | Objectif |
|---|---|
| Empreinte totale IT Flux | suivre la trajectoire |
| Top 5 applications émettrices | prioriser |
| Gains réalisés | prouver l’impact |
| Risques | anticiper les blocages |
| Projection -6 % / -20 % | piloter la trajectoire |
| Coût évité | relier GreenOps et FinOps |

### Gain attendu

Créer une gouvernance crédible et pilotable devant DSI, métiers, architecture, production et RSE.

---

## 5.14 Priorisation des leviers BPCE

| Priorité | Levier | Pourquoi |
|---:|---|---|
| 1 | Baseline carbone applicative | Sans mesure, aucun pilotage fiable. |
| 2 | Intensité carbone par transaction | Adapté aux flux bancaires à forte volumétrie. |
| 3 | Optimisation batch | Fort potentiel sur SCT, SDD, EOD. |
| 4 | Réduction logs/données | Quick win souvent sous-estimé. |
| 5 | Right-sizing | Gains rapides coût + carbone. |
| 6 | CI/CD responsable | Empêche la dette carbone future. |
| 7 | Green Weighting Factor IT | Priorise objectivement les chantiers. |
| 8 | Budget carbone IT | Stabilise la trajectoire long terme. |
| 9 | Formation squads | Rend la démarche durable. |
| 10 | Reporting direction | Donne de la visibilité et du pouvoir d’arbitrage. |

---

# 6. Courbe d’atteinte des objectifs

## 6.1 Leviers par phase

### Phase 1 (2019-2024)
- énergie
- infra
- immobilier

### Phase 2 (2024-2026)
- IT optimization
- batch
- logs

### Phase 3 (2026-2030)
- refonte applicative
- écoconception
- architecture

---

# 7. Plan d’action détaillé

## Étape 1
Mesurer

## Étape 2
Comparer

## Étape 3
Prioriser

## Étape 4
Optimiser

## Étape 5
Industrialiser

---

# 8. Conclusion

BPCE doit passer :

RSE → GreenOps opérationnel

👉 clé :
- mesure
- pilotage
- industrialisation

---

FIN

