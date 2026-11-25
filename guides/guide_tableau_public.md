# Guide outil – Tableau Public

## Connecter les données
1. Ouvrir Tableau Public.
2. Choisir un fichier texte/CSV et sélectionner `data/banking_dataset_anonymized.csv`.
3. Dans l'onglet Source de données, contrôler les types de champs.
4. Vérifier les champs date, nombres et dimensions.
5. Ne pas publier d'autres sources contenant des informations personnelles.

## Créer des feuilles
Créer une feuille par visualisation :
- KPI clients : `COUNTD([customer_ref])`.
- Volume transactions : `SUM([transaction_amount])`.
- Transaction moyenne : `AVG([transaction_amount])`.
- Clients par type de compte : `account_type` en lignes, `COUNTD(customer_ref)` en colonnes.
- Transactions dans le temps : `transaction_date` en colonnes, `SUM(transaction_amount)` en lignes.
- Prêts par type : `loan_type` et `SUM(loan_amount)` (après vérification de la granularité).
- Retours clients : `feedback_type` et nombre d'enregistrements.

## Exemples de champs calculés
Prêts approuvés :
`IF [loan_status] = "Approved" THEN 1 ELSE 0 END`

Réclamation :
`IF [feedback_type] = "Complaint" THEN 1 ELSE 0 END`

Retour résolu :
`IF [resolution_status] = "Resolved" THEN 1 ELSE 0 END`

Taux de prêts approuvés :
`SUM([Prêt approuvé]) / COUNT([loan_status])`

Taux de résolution :
`SUM([Retour résolu]) / COUNT([resolution_status])`

Formater les taux en pourcentage et traiter les valeurs nulles si nécessaire.

## Assembler les dashboards
1. Cliquer sur Nouveau tableau de bord.
2. Glisser-déposer les feuilles depuis le panneau.
3. Organiser les vues selon les trois pages du TP.
4. Ajouter les filtres et appliquer leur portée aux feuilles concernées.
5. Configurer les actions de filtre si elles sont utiles.
6. Régler les infobulles, titres, légendes et tailles.
7. Tester les filtres et interactions.

## Publier
1. Se connecter à Tableau Public.
2. Enregistrer sur Tableau Public.
3. Vérifier la publication et le lien.
4. Ajouter le lien dans `livrables/lien_dashboard.md`.

**Important :** Tableau Public est un espace public. La publication du classeur peut rendre les données sous-jacentes accessibles. Utiliser uniquement le CSV anonymisé fourni et vérifier le contenu avant publication.

Documentation : https://help.tableau.com/current/pro/desktop/en-us/default.htm
