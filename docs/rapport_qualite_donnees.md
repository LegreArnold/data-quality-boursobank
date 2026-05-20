# Rapport de Qualite des Donnees - BoursoBank


---

## 1. Contexte et Objectif

BoursoBank est une banque 100% digitale comptant plus de 8 millions de clients.
La totalite des operations clients transitent par le Systeme d'Information (SI).

Une mauvaise qualite des donnees dans le SI peut entrainer :
- Des erreurs de facturation client
- Des risques reglementaires (clients mineurs, identites inconnues)
- Des decisions strategiques basees sur des donnees incorrectes

**Objectif de cette analyse :** Verifier la conformite des donnees de transactions
aux regles de gestion metier definies et formuler des recommandations correctives.

---

## 2. Perimetre de l'Analyse

- **Dataset :** Synthetic Financial Payment System (Edgar Lopez-Rojas)
- **Volume :** 594 643 transactions
- **Periode :** Simulation sur 180 jours
- **Colonnes analysees :** customer, age, gender, amount, category, fraud

---

## 3. Regles de Gestion Appliquees

| Code | Type | Regle | Colonne |
|------|------|-------|---------|
| RG01 | Completude | ID client ne doit pas etre vide | customer |
| RG02 | Format | Age doit etre dans le referentiel defini | age |
| RG03 | Format | Genre doit etre M, F ou E uniquement | gender |
| RG04 | Coherence | Montant doit etre strictement superieur a 0 | amount |
| RG05 | Unicite | Chaque transaction doit etre unique | toutes |

---

## 4. Resultats de l'Analyse

### 4.1 Bilan Global

| Regle | Statut | Nombre d'anomalies | Criticite |
|-------|--------|-------------------|-----------|
| RG01 | CONFORME | 0 | - |
| RG02 | NON CONFORME | 61 761 | CRITIQUE |
| RG03 | NON CONFORME | 515 | MODERE |
| RG04 | NON CONFORME | 52 | MODERE |
| RG05 | CONFORME | 0 | - |

**Total anomalies detectees : 62 328 sur 594 643 transactions (10.5%)**

### 4.2 Detail des Anomalies

**RG02 - Anomalies sur l'age (61 761 anomalies)**
- 2 452 valeurs hors referentiel — probleme d'encodage dans le SI
- 58 131 transactions liees a des clients mineurs (tranche age '1')
- 1 178 transactions avec age inconnu ('U')

**RG03 - Anomalies sur le genre (515 anomalies)**
- 515 transactions avec genre inconnu ('U')
- Impact : impossible de verifier l'identite complete du client

**RG04 - Anomalies sur le montant (52 anomalies)**
- 52 transactions enregistrees avec un montant de 0€
- Toutes concentrees sur la categorie transport
- Hypothese : erreur de saisie sur les terminaux de paiement

### 4.3 Analyse Complementaire - Fraude par Categorie

Au-dela des regles de gestion, l'analyse revele une concentration
importante de fraudes sur certaines categories :

| Categorie | Taux de fraude | Montant moyen |
|-----------|---------------|---------------|
| es_leisure | 94.99% | 288.91€ |
| es_travel | 79.40% | 2 250.41€ |
| es_sportsandtoys | 49.53% | 215.72€ |
| es_food | 0.00% | 37.07€ |
| es_transportation | 0.00% | 26.96€ |

---

## 5. Recommandations

### Recommandation 1 - CRITIQUE
**Probleme :** 58 131 transactions liees a des clients potentiellement mineurs  
**Impact :** Risque reglementaire majeur — ouverture de comptes pour mineurs interdite  
**Action :** Audit immediat des comptes de tranche age '1' et verification des pieces d'identite

### Recommandation 2 - CRITIQUE  
**Probleme :** 2 452 valeurs d'age hors referentiel  
**Impact :** Donnees inutilisables pour les reportings reglementaires  
**Action :** Correction de l'encodage dans le SI et mise en place d'un controle a la saisie

### Recommandation 3 - MODERE
**Probleme :** 515 clients avec genre inconnu  
**Impact :** Identification client incomplete  
**Action :** Campagne de mise a jour des profils clients concernés

### Recommandation 4 - MODERE
**Probleme :** 52 transactions a 0€ sur le transport  
**Impact :** Erreurs d'enregistrement dans le SI  
**Action :** Mise en place d'un controle bloquant sur les terminaux — montant minimum 0.01€

### Recommandation 5 - PREVENTIF
**Probleme :** Concentration des fraudes sur loisirs et voyages  
**Impact :** Risque financier eleve sur ces categories  
**Action :** Renforcer l'authentification pour toute transaction superieure a 100€
dans les categories loisirs et voyages

---

## 6. Conclusion

L'analyse de 594 643 transactions revele un taux d'anomalies de 10.5%.
Les anomalies les plus critiques concernent les transactions liees a des
clients mineurs — un risque reglementaire qui necessite une action immediate.

Les recommandations formulees permettront a BoursoBank de :
- Reduire le risque reglementaire
- Ameliorer la fiabilite des donnees du SI
- Renforcer la detection des transactions frauduleuses