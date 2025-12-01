# Talend_ETL_Snowflake_Expense_Data
# Projet ETL : Ingestion de Données de Dépenses avec Talend et Snowflake  

Description du Projet :

Ce projet met en œuvre un pipeline ETL complet pour l'intégration de données de suivi de dépenses, depuis un fichier source Excel se trouvant dans Google Drive jusqu'à un Entrepôt de Données hébergé sur Snowflake. 

L'objectif principal est de structurer les données brutes dans des schémas optimisés pour l'analyse (ODS et DWH) et d'automatiser le processus d'ingestion. 

 
Architecture du Data Warehouse :

L'EDD sur Snowflake  est séparé en deux schémas pour une gestion structurée de la donnée : 

--> Schéma ODS (Operational Data Store) 

Objectif : Stockage temporaire des données brutes après l'extraction, avec une structure similaire aux feuilles du fichier source. 

Jobs d'alimentation : 

- JCategorie_FILE_ODS  

- JDepense_FILE_ODS 

- JGoogleDriveGet_FILE_ODS 

- JMasterODS 

- JSousCategorie_FILE_ODS 


--> Schéma DWH (Data Warehouse)  

Objectif : Stockage des données modélisées selon un modèle dimensionnel pour l'analyse. 

Jobs d'alimentation : 

- jDimCategorie_ODS_DWH 

- jDimDate_ODS_DWH 

- jDimDescriptionDepense_ODS_DWH 

- jDimSousCategorieDepense_ODS_DWH 

- jFactDepense_ODS_DWH 

- JMasterDWH 

Le pipeline complet est orchestré via un Job Master (exécutable via .bat pour windows) qui : 

Exécute les scripts SQL de création des tables ODS et DWH sur Snowflake. 

Exécute les Jobs ODS pour l'ingestion initiale des données du fichier source. 

Exécute les Jobs DWH pour la transformation et le chargement des données dimensionnelles et factuelles. 

L'utilisation de variables de contexte a été systématisée pour les paramètres de connexion à la base de données, le chemin d'accès et le nom du fichier source. 
