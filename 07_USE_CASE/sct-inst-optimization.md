# Use Case — Optimisation SCT Inst

## Problème

Flux temps réel avec latence critique. Toute saturation entraîne timeouts, retries, logs et surconsommation.

## Modèles mobilisés

- Files d’attente ;
- P95/P99 ;
- retries/timeouts ;
- multi-objectifs.

## Actions

- mesurer λ, μ, P95/P99 ;
- dimensionner les pods / workers ;
- limiter retries ;
- isoler contrôles non critiques en asynchrone ;
- suivre gCO2e / SCT Inst.
