# Questions / réponses entretien

## Pourquoi parler de recherche opérationnelle ?

Parce que le problème est une optimisation sous contraintes : carbone, coût, SLA, capacité, risque. La RO donne un cadre rationnel pour arbitrer.

## Comment atteindre -6 % fin 2026 ?

Par quick wins mesurables : extinction non-prod, right-sizing, logs, retries, batchs inutiles. Les gains doivent être validés par baseline.

## Comment éviter de dégrader la production ?

Par pilote, mesure avant/après, rollback, validation architecture/production et contraintes SLA intégrées.

## Quel lien entre SonarQube/Checkmarx et GreenOps ?

La dette technique et les vulnérabilités créent incidents, reprises, erreurs, corrections urgentes et instabilité. Cela se traduit souvent par plus de CPU, logs et consommation.

## Pourquoi commencer par la baseline ?

Sans baseline, les gains ne sont pas démontrables et les décisions sont fragiles.

## Pourquoi l’EDA ?

Pour réduire polling, couplage et charge inutile sur DB/API, sans toucher au chemin synchrone critique quand ce n’est pas pertinent.
