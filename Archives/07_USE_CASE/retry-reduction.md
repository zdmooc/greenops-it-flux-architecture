# Use Case — Réduction des retries

## Problème

Les retries excessifs consomment CPU, augmentent les logs, saturent les services et dégradent la latence.

## Modèle

```text
N_total = N(1+r)
E_total = e × N(1+r)
CO2_total = c × N(1+r)
```

## Actions

- mesurer le taux retry par application ;
- distinguer erreurs transitoires/permanentes ;
- appliquer backoff ;
- limiter retries ;
- introduire circuit breaker ;
- mesurer avant/après.
