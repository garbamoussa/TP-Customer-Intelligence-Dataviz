# Guide outil – Looker Studio

## Préparer la source
1. Ouvrir le fichier `data/banking_dataset_anonymized.csv`.
2. L'importer dans Google Sheets (Fichier > Importer > Importer).
3. Vérifier les dates, les nombres et les en-têtes. Une ligne doit correspondre à une observation du fichier.
4. Nommer clairement l'onglet, par exemple `banking_data`.

## Créer le rapport
1. Ouvrir https://lookerstudio.google.com/.
2. Créer > Rapport.
3. Ajouter des données > Google Sheets.
4. Sélectionner le classeur et l'onglet contenant les données.
5. Vérifier les types et agrégations dans la source de données.

## Construire les composants
- Carte de score : clients distincts (`COUNT_DISTINCT(customer_ref)`).
- Carte de score : volume des transactions (`SUM(transaction_amount)`).
- Carte de score : transaction moyenne (`AVG(transaction_amount)`).
- Graphique en barres : dimension `account_type`, métrique nombre distinct de clients.
- Série temporelle : dimension `transaction_date`, métrique somme des montants.
- Contrôle de période : utiliser `transaction_date`.
- Listes déroulantes : `city`, `account_type`, `loan_type`, `feedback_type`.

## Champs calculés – exemples
Nombre distinct de clients :
`COUNT_DISTINCT(customer_ref)`

Nombre de prêts approuvés (sur les lignes disponibles) :
`SUM(CASE WHEN loan_status = "Approved" THEN 1 ELSE 0 END)`

Part des prêts approuvés :
`SUM(CASE WHEN loan_status = "Approved" THEN 1 ELSE 0 END) / COUNT(loan_status)`

Nombre de réclamations :
`SUM(CASE WHEN feedback_type = "Complaint" THEN 1 ELSE 0 END)`

Part des retours résolus :
`SUM(CASE WHEN resolution_status = "Resolved" THEN 1 ELSE 0 END) / COUNT(resolution_status)`

Formater les ratios en pourcentage. Vérifier les valeurs nulles et la granularité avant de présenter ces taux.

## Mise en page
- Page 1 : Vue d'ensemble.
- Page 2 : Activité client et transactions.
- Page 3 : Crédits et relation client.
- Ajouter un titre, une note de source et une période.
- Aligner les graphiques et limiter les couleurs.
- Tester chaque contrôle avec plusieurs valeurs.

## Vérification avant partage
- Les KPI changent-ils lorsque les filtres changent ?
- Les dates sont-elles triées chronologiquement ?
- Les montants ont-ils la bonne devise/unité ?
- Les graphiques affichent-ils des valeurs nulles ou aberrantes ?
- Le lien est-il accessible en lecture aux personnes visées ?

Documentation : https://cloud.google.com/looker/docs/studio
