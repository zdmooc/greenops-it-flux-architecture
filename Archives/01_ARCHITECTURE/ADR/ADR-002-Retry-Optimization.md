# ADR-002 — Retry-aware architecture

## Décision

Standardiser les politiques de retries, timeouts, backoff et circuit breaker.

## Motivation

Les retries non maîtrisés consomment CPU, logs, stockage et augmentent la latence.

## Règles

- différencier erreur transitoire et permanente ;
- limiter le nombre de retries ;
- appliquer un backoff ;
- isoler les dégradations avec circuit breaker ;
- mesurer le taux retry comme KPI GreenOps.
