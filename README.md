# TP – Customer Intelligence : création d'un dashboard Dataviz

**Niveau :** Master  
**Outils au choix :** Looker Studio ou Tableau Public  
**Durée indicative :** 6 à 8 heures  
**Contexte :** Customer Intelligence dans le secteur bancaire

## 1. Mission

Vous êtes analyste de données dans une banque. La direction souhaite disposer d'un tableau de bord permettant de comprendre la clientèle, l'activité transactionnelle, les produits de crédit et la qualité de service.

Votre mission est de construire un dashboard clair, fiable et interactif. Le travail porte prioritairement sur la prise en main de l'outil de Dataviz : connexion à la source, dimensions et mesures, champs calculés, graphiques, filtres, interactions, mise en page et publication.

**Aucun travail de Prompt Engineering n'est demandé.**

## 2. Données fournies

Fichier : `data/banking_dataset_anonymized.csv`

Le fichier est une version de travail du dataset bancaire fourni pour le TP. Les colonnes permettant d'identifier directement une personne (nom, prénom, adresse postale, téléphone, e-mail) ont été retirées. La clé client est pseudonymisée.

Le fichier contient des observations relatives aux clients, comptes, transactions, crédits, cartes et retours clients. Les étudiants doivent vérifier la granularité et les valeurs avant de construire les indicateurs.

> Données pédagogiques : ne pas tenter de réidentifier les personnes. Ne pas ajouter de données personnelles. Pour Tableau Public, ne publier que le fichier anonymisé fourni dans ce dépôt.

## 3. Objectifs opérationnels

À la fin du TP, vous devez savoir :
- connecter un fichier CSV ou Google Sheets ;
- distinguer dimensions et mesures ;
- choisir une agrégation correcte (somme, moyenne, compte distinct, etc.) ;
- créer des champs calculés ;
- construire des graphiques adaptés à une question métier ;
- assembler plusieurs vues dans un dashboard ;
- ajouter des filtres, contrôles et interactions ;
- améliorer la lisibilité et la hiérarchie visuelle ;
- publier et partager un résultat.

## 4. Travail demandé

### Partie A – Prise en main et connexion des données
1. Ouvrir l'outil choisi.
2. Connecter `banking_dataset_anonymized.csv` (Tableau Public) ou importer le CSV dans Google Sheets puis connecter la feuille à Looker Studio.
3. Vérifier les types de champs : texte, nombre, date.
4. Repérer les dimensions et mesures.
5. Vérifier les agrégations proposées automatiquement.
6. Renommer les champs affichés si nécessaire.

**À rendre :** une capture d'écran de la source de données et une courte liste de 10 dimensions/mesures utiles.

### Partie B – Construire les indicateurs
Créer au minimum les indicateurs suivants, en adaptant les formules à l'outil :

| Indicateur | Définition |
|---|---|
| Clients distincts | Nombre distinct de `customer_ref` |
| Solde moyen | Moyenne de `account_balance` |
| Volume des transactions | Somme de `transaction_amount` |
| Nombre de transactions | Nombre d'enregistrements avec une transaction |
| Transaction moyenne | Moyenne de `transaction_amount` |
| Montant total des prêts | Somme de `loan_amount` |
| Taux de prêts approuvés | Part des lignes dont `loan_status` vaut Approved |
| Réclamations | Nombre de lignes dont `feedback_type` vaut Complaint |
| Taux de résolution | Part des retours dont `resolution_status` vaut Resolved |
| Points de fidélité moyens | Moyenne de `rewards_points` |

**Attention à la granularité :** le fichier peut contenir plusieurs lignes pour un même client. Ne pas additionner un solde de compte ou un montant de prêt répété sur plusieurs lignes sans vérifier la structure. Utiliser un comptage distinct pour les clients. Expliquer les limites des indicateurs calculés à partir de lignes répétées.

### Partie C – Construire les visualisations
Construire au moins les vues suivantes :

1. **Carte KPI** : clients distincts.
2. **Carte KPI** : volume des transactions.
3. **Carte KPI** : solde moyen.
4. **Histogramme** : nombre de clients par type de compte.
5. **Barres** : transactions par type de transaction.
6. **Courbe temporelle** : montant des transactions par date.
7. **Barres** : montants de prêts par type de prêt.
8. **Graphique** : répartition des statuts de prêts.
9. **Barres** : retours clients par type de feedback.
10. **Graphique** : statuts de résolution des retours.

Pour chaque graphique, donner un titre explicite et vérifier que le type de graphique répond à la question posée. Éviter les graphiques 3D et les effets décoratifs inutiles.

### Partie D – Assembler le dashboard
Créer un dashboard composé de trois zones ou pages :

**Page 1 – Vue d'ensemble**
- titre et période étudiée ;
- 3 à 4 KPI ;
- répartition par type de compte ;
- activité transactionnelle ;
- filtre sur la ville et le type de compte.

**Page 2 – Activité client et transactions**
- évolution temporelle des transactions ;
- répartition par type de transaction ;
- comparaison des villes ;
- filtre sur la ville, le genre et la période.

**Page 3 – Crédits et relation client**
- montants par type de prêt ;
- statuts de prêts ;
- retours clients par catégorie ;
- statuts de résolution ;
- filtre sur le type de prêt et le type de feedback.

Les filtres doivent être testés : vérifier qu'ils modifient les graphiques attendus et qu'ils ne créent pas de résultats incohérents.

### Partie E – Mise en forme et publication
- utiliser une palette cohérente et accessible ;
- aligner les composants et harmoniser les tailles ;
- limiter le nombre de couleurs ;
- afficher les unités et périodes ;
- ajouter une date de mise à jour ou une note sur la source ;
- tester le dashboard sur différentes tailles d'écran ;
- publier ou partager le dashboard selon les règles de l'outil.

## 5. Parcours Looker Studio

1. Importer le CSV dans Google Sheets.
2. Dans Looker Studio, créer un rapport vierge.
3. Ajouter une source de données Google Sheets.
4. Vérifier les types des champs et les agrégations.
5. Ajouter les graphiques depuis la barre d'outils.
6. Ajouter les cartes de score pour les KPI.
7. Créer les champs calculés dans la source ou dans le graphique.
8. Ajouter des contrôles : liste déroulante, période, recherche.
9. Organiser les pages et appliquer un thème.
10. Tester le rapport puis partager le lien en lecture.

Documentation officielle : https://cloud.google.com/looker/docs/studio

## 6. Parcours Tableau Public

1. Ouvrir Tableau Public et créer un classeur.
2. Se connecter au fichier CSV.
3. Vérifier les types de données dans la source.
4. Créer les feuilles (*Worksheets*) une par une.
5. Utiliser `COUNTD(customer_ref)` pour le nombre distinct de clients.
6. Créer les champs calculés nécessaires.
7. Assembler les feuilles dans des dashboards.
8. Ajouter des filtres et choisir leur portée.
9. Tester les actions de filtre et les infobulles.
10. Publier sur Tableau Public et récupérer le lien.

Documentation officielle : https://help.tableau.com/current/pro/desktop/en-us/default.htm

**Confidentialité :** Tableau Public rend les classeurs publiés accessibles publiquement. Ne publier aucune donnée personnelle, confidentielle ou réelle non autorisée.

## 7. Questions métier à traiter

À partir du dashboard, répondre en quelques lignes :
1. Quel type de compte est le plus représenté ?
2. Quels types de transactions contribuent le plus au volume ?
3. Comment l'activité évolue-t-elle dans le temps ?
4. Quels types de prêts sont les plus présents ?
5. Quelle est la part des prêts approuvés ?
6. Quels types de retours clients sont les plus fréquents ?
7. Quel est le niveau de résolution des retours ?
8. Quelles sont les deux limites principales des données ou des indicateurs ?

## 8. Livrables attendus

- lien de partage du dashboard ;
- fichier de travail Tableau (`.twb` ou `.twbx`) si Tableau est choisi ;
- copie ou lien du Google Sheet utilisé si Looker Studio est choisi ;
- 3 à 5 captures d'écran ;
- réponses aux questions métier (2 pages maximum) ;
- courte fiche indiquant les champs calculés créés et les filtres utilisés.

## 9. Barème – 20 points

| Critère | Points |
|---|---:|
| Connexion et paramétrage de la source | 3 |
| Dimensions, mesures et agrégations | 3 |
| KPI et champs calculés | 3 |
| Choix et construction des graphiques | 4 |
| Organisation et lisibilité du dashboard | 3 |
| Filtres et interactions | 2 |
| Publication et interprétation métier | 2 |
| **Total** | **20** |

## 10. Arborescence du dépôt

```text
TP-Customer-Intelligence-Dataviz/
├── README.md
├── data/
│   └── banking_dataset_anonymized.csv
├── guides/
│   ├── guide_looker_studio.md
│   └── guide_tableau_public.md
└── livrables/
    ├── captures/
    ├── lien_dashboard.md
    └── analyse_metier.md
```

## 11. Consigne finale

Le dashboard sera évalué sur sa capacité à rendre les données compréhensibles et à faciliter une décision. Un dashboard n'est pas une collection de graphiques : chaque composant doit avoir une fonction, un indicateur doit avoir une définition claire et chaque filtre doit avoir un comportement vérifié.
