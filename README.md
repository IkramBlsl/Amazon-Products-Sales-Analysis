# 📊 Sales Analysis Dashboard – Amazon Products (Power BI)

## 📝 Description

Ce dashboard interactif fournit une analyse détaillée des ventes de produits Amazon. Il permet d’évaluer les performances commerciales sur différentes périodes (année, trimestre, semaine), de surveiller les tendances de vente, et d’identifier les produits les plus vendus et les mieux évalués par les clients.


## 📌 Problem Statement

L’objectif principal est de suivre et d’évaluer les performances commerciales sur plusieurs dimensions :

    📅 Suivi des ventes en temps réel (YTD & QTD)

    📦 Analyse du nombre de produits vendus

    ⭐ Suivi des avis clients pour mesurer la satisfaction

    📈 Compréhension des tendances hebdomadaires et mensuelles

    🏆 Identification des produits générateurs de chiffre d'affaires

## 🧮 KPI's définis

| KPI                   | Objectif                                              |
| --------------------- | ----------------------------------------------------- |
| **YTD Sales**         | Suivre les ventes cumulées depuis le début de l'année |
| **QTD Sales**         | Évaluer les ventes sur le trimestre en cours          |
| **YTD Products Sold** | Analyser le volume de produits vendus cette année     |
| **YTD Reviews**       | Mesurer les retours clients via les avis produits     |


## 📊 Visualisations

| Visualisation                                 | Objectif                                            |
| --------------------------------------------- | --------------------------------------------------- |
| **Line Chart – YTD Sales by Month**           | Identifier les tendances mensuelles et saisonnières |
| **Column Chart – YTD Sales by Week**          | Observer les fluctuations hebdomadaires             |
| **Heatmap/Text – Sales by Product Category**  | Vue globale de la performance par catégorie         |
| **Bar Chart – Top 5 Products by YTD Sales**   | Identifier les produits les plus rentables          |
| **Bar Chart – Top 5 Products by YTD Reviews** | Mettre en avant les produits les plus appréciés     |

## 📁 Structure des données

### 🔹 Table principale : Amazon_Data

    Order Date, Price(Dollar), Product Category

    Product Description, Shipment, Number of Reviews

### 🔹 Table de dates personnalisée : Date Table

    Ajoutée via DAX :
    Date Table = CALENDAR(MIN(Amazon_Data[Order Date]), MAX(Amazon_Data[Order Date]))
    Colonnes dérivées :
    Month Name = FORMAT('Date Table'[Date] , "MMM")
    Month Number = MONTH('Date Table'[Date])
    Quarter Number = QUARTER('Date Table'[Date])
    Qtr = CONCATENATE("Qtr" , 'Date Table'[Quarter Number])
    Week = WEEKNUM('Date Table'[Date])

## 🧮 Measures personnalisées (DAX)

YTD Sales = TOTALYTD(SUM(Amazon_Data[Price(Dollar)]), 'Date Table'[Date])

QTD Sales = TOTALQTD(SUM(Amazon_Data[Price(Dollar)]), 'Date Table'[Date])

YTD Products Sold = TOTALYTD(COUNT(Amazon_Data[Product Category]), 'Date Table'[Date])

YTD Reviews = TOTALYTD(SUM(Amazon_Data[Number of reviews]), 'Date Table'[Date])
