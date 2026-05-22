# ⚽ Football Data Engineering avec PySpark : Statistiques, KPIs et Champions

## 📝 Présentation du Projet
Ce projet consiste à concevoir et implémenter un pipeline de données distribué avec **PySpark**. L'objectif est d'ingérer, nettoyer et analyser un historique de matchs de football afin de calculer des statistiques de performance avancées par équipe, générer un classement dynamique par saison et stocker les résultats sous un format hautement optimisé pour le Big Data.

## 🎯 Objectifs du Projet
* **Pipeline Big Data** : Bâtir un flux de traitement distribué robuste de bout en bout avec PySpark.
* **Calculs de KPIs Métier** : Manipuler les jointures, les agrégations complexes et les fonctions de fenêtrage (`Window`, `rank`).
* **Optimisation du Stockage** : Maîtriser l'écriture de fichiers au format **Parquet** et appliquer des stratégies de partitionnement.
* **Data Visualization** : Extraire les données agrégées pour concevoir des visualisations claires sur les performances des champions.

## 🛠️ Stack Technique
* **Framework de Calcul** : Apache Spark (PySpark).
* **Environnement de Développement** : Jupyter Notebook / Google Colab.
* **Format de Stockage** : Apache Parquet.
* **Librairies Python** : Pandas, Matplotlib, Seaborn (pour la restitution visuelle).
* **Gestion de Projet** : Jira & GitHub.

---

## 🏗️ Architecture du Pipeline ELT

Le traitement de données est orchestré selon les étapes suivantes :
1. **Ingestion** : Chargement du dataset brut au format CSV dans l'environnement Spark.
2. **Transformation & Traitement** : 
   * Nettoyage, gestion des types (`casts`) et calcul des colonnes de résultats (Victoire/Nul/Défaite).
   * Agrégations par équipe et par saison (Buts marqués, encaissés, pourcentage de victoires).
   * Application d'une logique de classement (*Ranking*) basée sur le pourcentage de victoires, puis sur le goal-différentiel.
3. **Stockage Optimisé** : Exportation des résultats globaux en Parquet partitionné par saison et des champions isolés.

---

## 🚀 Étapes de Réalisation

### 1. Ingestion et Préparation des Données 📥
* Initialisation de la session Spark et chargement du fichier source.
* Analyse du schéma, correction des types de données et gestion des valeurs manquantes.
* Création de colonnes indicatrices pour identifier le résultat de chaque match (Domicile / Extérieur / Nul).

### 2. Calcul des KPIs et Statistiques Équipe 📈
* Groupement des données par équipe et par saison (`groupBy`).
* Calcul cumulé des points, du nombre total de matchs joués, des victoires, des buts marqués, des buts encaissés et du *Goal Differential*.
* Calcul dynamique du pourcentage de victoires (*Win Percentage*).

### 3. Fenêtrage et Couronnement des Champions 🏆
* Définition d'une spécification de fenêtre (`Window.partitionBy("Season").orderBy(...)`).
* Attribution d'un rang exact (`TeamPosition`) pour classer rigoureusement toutes les équipes au sein de chaque saison.
* Filtrage et extraction des équipes ayant terminé à la première position afin d'isoler la table des champions (`football_top_teams`).

### 4. Stockage et Restitution Visuelle 💾
* Sauvegarde du dataset complet sous format **Parquet**, optimisé et partitionné par la colonne `Season`.
* Conversion des indicateurs clés vers Pandas pour générer des graphiques (Matplotlib/Seaborn) illustrant la domination des champions à travers le temps.

---

## 📦 Livrables
1. **Notebook Colab/Jupyter** : Code source PySpark entièrement commenté et structuré, sans chemins d'accès codés en dur.
2. **Datasets Parquet Générés** :
   * `football_stats_partitioned` : Toutes les statistiques d'équipes, partitionnées par saison.
   * `football_top_teams` : La liste exclusive des champions de chaque saison.
3. **Graphiques Analytics** : Visualisations des métriques clés (*WinPercentage*, buts marqués, *Goal Differentials*).
---
