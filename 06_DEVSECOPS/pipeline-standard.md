# Pipeline standard CI/CD

```text
Commit / MR
→ Build
→ Tests unitaires
→ SonarQube
→ Checkmarx
→ Package
→ Déploiement contrôlé
→ Smoke tests
→ Monitoring post-déploiement
```

## Règles

- Tout dépôt actif doit avoir un pipeline.
- SonarQube et Checkmarx sont intégrés par vagues.
- Les exceptions sont documentées.
- Les quality gates critiques deviennent progressivement bloquants.
