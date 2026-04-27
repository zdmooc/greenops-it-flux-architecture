# Modèles mathématiques et analytiques pour l’optimisation GreenOps

## 1. Modèles de mesure de base

### Intensité carbone applicative

```text
Carbone total = Énergie consommée × Intensité carbone de l’électricité + part matérielle
```

Normalisations :

- gCO2e / transaction ;
- gCO2e / batch ;
- gCO2e / API call ;
- gCO2e / 1000 transactions.

Utilité : comparer les applications, suivre -6 % / -20 %, prioriser.

### SCI

```text
SCI = ((E × I) + M) / R
```

Avec :

- E : énergie consommée ;
- I : intensité carbone ;
- M : empreinte matérielle allouée ;
- R : unité fonctionnelle.

### Consommation énergétique

Décomposer l’énergie en CPU, RAM, stockage, réseau, environnement.

## 2. Performance et capacité

### Files d’attente

Variables :

```text
λ = taux d’arrivée
μ = taux de service
c = nombre de serveurs / pods / workers
ρ = taux d’occupation
```

Formules M/M/1 :

```text
ρ = λ / μ
λ < μ
W = 1 / (μ - λ)
Wq = λ / (μ(μ - λ))
```

### Loi de Little

```text
L = λ × W
```

Permet de relier backlog, throughput et délai.

### Charge / capacité

Suivre charge moyenne, pointe, P95/P99 et marge de sécurité.

### Scaling

Scaling basé sur CPU, mémoire, QPS, backlog Kafka, latence ou profondeur de file.

## 3. Optimisation opérationnelle

### Right-sizing

Comparer : ressources allouées, consommées, marge utile, gaspillage.

### Multi-objectifs

```text
min αC(x) + βK(x) + γL(x) + δR(x)
```

Avec carbone, coût, latence, risque.

### Coût / performance / carbone

Pour chaque action : gain carbone, gain coût, impact performance, risque, effort, délai.

### Priorisation

```text
Score = (Impact × Faisabilité × Rapidité) / Risque
```

## 4. Flux et paiements

### Volumétrie transactionnelle

Transactions/jour, pics horaires, saisonnalité, retries, rejets, retraitements.

### STP / non-STP

Mesurer taux de traitement direct, intervention manuelle, reprise, rejet.

### Retries / timeouts

```text
N_total = N(1+r)
E_total = e × N(1+r)
CO2_total = c × N(1+r)
Logs_total = l × N(1+r)
```

Variante :

```text
E_total = N e0 + N r er
```

### Synchrone vs asynchrone

Comparer polling, callbacks, événements Kafka, charge DB/API.

## 5. Données / stockage / logs

### Croissance des données

Croissance journalière, rétention, chaud/tiède/froid, volume archivé.

### Logs

Logs par transaction, logs utiles, logs redondants, coût stockage/indexation, CPU Elastic/Logstash.

### Optimisation SQL

Coût requête, temps CPU, I/O, cardinalité, fréquence d’exécution.

## 6. Fiabilité et résilience

SLA, SLI, SLO, MTBF, MTTR, risque opérationnel, coût de non-qualité.

## 7. CI/CD et qualité

Couverture pipeline, SonarQube, Checkmarx, quality gates, dette technique, corrélation qualité/performance/carbone.

## 8. Modèles avancés

- Régression statistique ;
- analyse de sensibilité ;
- simulation de scénarios ;
- optimisation sous contraintes ;
- Pareto 80/20.

## 9. Modèles à prioriser

### Niveau 1

SCI, intensité carbone applicative, charge/capacité, files d’attente, right-sizing, retries/timeouts, volumétrie transactionnelle, logs, priorisation, coût-carbone-performance.

### Niveau 2

Régression, sensibilité, scénarios, Pareto, multi-objectifs.
