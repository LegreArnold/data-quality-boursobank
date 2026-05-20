## Data Quality Analyst - BoursoBank

Projet Business Analyst - Analyse de la qualite des donnees de transactions bancaires.

## Probleme Metier

Comment garantir que les donnees qui circulent dans le SI de BoursoBank
sont completes, coherentes et fiables avant qu'elles causent des dommages
clients, reglementaires ou decisionnels ?

## Resultats Cles

| Regle | Type | Anomalies | Criticite |
|-------|------|-----------|-----------|
| RG01 - ID Client | Completude | 0 | Conforme |
| RG02 - Age | Format | 61 761 | CRITIQUE |
| RG03 - Genre | Format | 515 | Modere |
| RG04 - Montant | Coherence | 52 | Modere |
| RG05 - Doublons | Unicite | 0 | Conforme |

**10.5% des transactions presentent au moins une anomalie**

## Recommandations Principales

- Audit immediat des 58 131 comptes clients mineurs
- Correction de l'encodage age dans le SI
- Authentification renforcee pour transactions loisirs et voyages superieures a 100€

## Stack Technique

- Python - Pandas - Jupyter Notebook
- Git / GitHub
- Power BI 

## Structure du Projet

- notebooks/ - Analyse et regles de gestion
- outputs/ - Visualisations
- docs/ - Rapport de qualite et documentation

## Dataset

Source : Synthetic Financial Payment System - Edgar Lopez-Rojas
594 643 transactions bancaires europeennes
