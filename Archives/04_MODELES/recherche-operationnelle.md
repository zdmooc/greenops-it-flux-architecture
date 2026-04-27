# Recherche opérationnelle appliquée au GreenOps IT Flux

## Pourquoi la RO est clé

Le sujet est une optimisation multi-contrainte : minimiser CO2, coût et gaspillage sous contraintes SLA, disponibilité, capacité et délais.

## Modèles utiles

| Modèle | Usage |
|---|---|
| Programmation linéaire | allocation ressources |
| PLNE | décisions ON/OFF, nombre pods/VM |
| Multi-objectifs | arbitrage carbone/coût/SLA/risque |
| Network flow | optimisation flux API/Kafka/MFT |
| Files d’attente | latence et dimensionnement |
| Scheduling | batchs et carbon-aware scheduling |
| Knapsack | priorisation quick wins |
| Localisation/allocation | placement datacenter/cluster/cloud |
| Optimisation sous incertitude | pics et variabilité |
| Monte Carlo | simulation de scénarios |

## PLNE — right-sizing / extinction

Variables :

```text
xi ∈ {0,1} : environnement actif ou non
yj ∈ N : nombre de pods / VM / instances
```

Objectif :

```text
min Σ Ci xi + Σ Rj yj
```

Contraintes :

```text
Σ Capj yj ≥ Demand
Latency(yj) ≤ SLAmax
Σ yj ≥ Redundancymin
```

## Scheduling — batchs

Objectif :

```text
min Σ Ek × I(tk)
```

Contraintes :

```text
tk ∈ [startk, endk]
tk + durationk ≤ tk+1
Σ Loadk(t) ≤ Capacity
```

## Knapsack — priorisation

Objectif :

```text
max Σ Gainm × zm
```

Contraintes :

```text
Σ Costm × zm ≤ Budget
Σ Riskm × zm ≤ Riskmax
```

## Multi-objectifs

```text
min αC(x) + βK(x) + γL(x) + δR(x)
```

ou :

```text
min C(x)
subject to:
L(x) ≤ SLAmax
K(x) ≤ Budget
R(x) ≤ Riskmax
```

## Message entretien

> J’utilise la recherche opérationnelle pour optimiser le SI sous contraintes carbone, SLA, coût, capacité et risque.
