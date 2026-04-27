# GreenOps Tools Canvas — Mesure carbone IT & Architecture

---

## 1. Objectif
Ce document présente les outils permettant de :
- mesurer l’énergie IT
- convertir en CO₂
- piloter GreenOps
- industrialiser en entreprise

---

## 2. Vue d’ensemble des outils

| Famille | Objectif | Outils |
|---|---|---|
| Mesure locale | énergie machine | Scaphandre |
| Kubernetes | énergie pods | Kepler |
| Observabilité | métriques | Prometheus / Grafana |
| Conversion CO2 | calcul carbone | Impact Framework |
| Benchmark | test appli | Green Metrics Tool |
| Cloud carbone | estimation cloud | Cloud Carbon Footprint |
| Green IT entreprise | pilotage SI | Aguaro / Sopht |
| FinOps | coût + usage | Apptio / Flexera |
| ESG | reporting groupe | Greenly / Plan A |

---

## 3. Scaphandre (mesure PC / serveur)
- mesure watts CPU
- attribution aux processus
- export Prometheus

Commande :
scaphandre prometheus

---

## 4. Kepler (Kubernetes)
pods / containers / nodes

---

## 5. Prometheus + Grafana
collecte + visualisation

---

## 6. Impact Framework
CO2 = kWh × facteur carbone

---

## 7. Green Metrics Tool
benchmark applicatif

---

## 8. Cloud Carbon Footprint
estimation cloud

---

## 9. Boavizta
impact matériel

---

## 10. Observabilité
CPU / RAM / latence

---

## 11. Aguaro / Sopht
pilotage entreprise

---

## 12. FinOps Tools
coût + carbone

---

## 13. ESG Tools
reporting CSRD

---

## 14. Stack locale

PC → Scaphandre → Prometheus → Grafana → CO2

---

## 15. Stack Kubernetes

K8s → Kepler → Prometheus → Grafana → CO2

---

## 16. KPI clés

- gCO2e / transaction
- kgCO2e / batch
- tCO2e / application

---

## 17. Conclusion

GreenOps = Mesure → Conversion → Analyse → Pilotage
