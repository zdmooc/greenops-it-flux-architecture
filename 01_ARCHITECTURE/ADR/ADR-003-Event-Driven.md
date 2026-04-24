# ADR-003 — Événementialisation progressive

## Décision

Réduire progressivement le polling au profit d’une architecture événementielle lorsque le cas d’usage le permet.

## Motivation

Le polling génère des appels inutiles, de la charge DB/API et du gaspillage énergétique.

## Conséquences

- Identification des flux candidats.
- Priorité aux traitements asynchrones et post-traitements.
- Protection des flux synchrones critiques SCT Inst.
