
# Energy Consumption Prediction

## Présentation

Ce projet a pour objectif d'analyser et de prévoir la consommation énergétique d'un logement à partir de données environnementales et temporelles.

Le projet a été réalisé dans le cadre de mon apprentissage en Data Science et Machine Learning. Il m'a permis de travailler sur l'exploration de données, le feature engineering, la comparaison de modèles de régression et la validation de modèles sur des données temporelles.

## Données

Le dataset contient environ 20 000 observations enregistrées toutes les 10 minutes.

La variable cible est :

- `Appliances` : consommation énergétique des appareils électriques.

Les variables disponibles comprennent notamment :

- températures intérieures et extérieures ;
- taux d'humidité ;
- pression atmosphérique ;
- vitesse du vent ;
- éclairage ;
- variables temporelles.

## Étapes du projet

### 1. Exploration des données

- Analyse de la structure du dataset
- Vérification des valeurs manquantes
- Analyse statistique de la consommation
- Étude de la distribution et des valeurs extrêmes
- Analyse des corrélations

### 2. Feature engineering

Création de plusieurs variables temporelles :

- heure de la journée ;
- jour de la semaine ;
- mois ;
- indicateur week-end.

Une deuxième partie du projet a été consacrée à la prévision temporelle avec la création de :

- lag features ;
- moyennes glissantes ;
- variables historiques de consommation.

### 3. Modélisation classique

Deux modèles ont d'abord été comparés :

- Régression linéaire
- Random Forest

Sur une séparation aléatoire des données, le Random Forest a obtenu de meilleures performances que la régression linéaire.

### 4. Validation temporelle

Une validation avec `TimeSeriesSplit` a ensuite montré que les performances diminuaient fortement lorsque l'ordre chronologique des données était respecté.

Cette observation m'a amenée à reformuler le problème comme un problème de prévision temporelle.

### 5. Forecasting

Plusieurs approches ont été testées :

- baseline naïve basée sur la consommation précédente ;
- Random Forest avec lag features ;
- Random Forest avec variables temporelles enrichies ;
- Gradient Boosting.

La baseline naïve s'est révélée plus performante que les modèles plus complexes sur la période de test.

Ce résultat montre que la consommation présente une forte dépendance aux observations très récentes.

## Résultats principaux

### Modélisation classique

La régression linéaire obtenait des performances limitées, tandis que le Random Forest donnait de meilleurs résultats sur une séparation aléatoire des données.

### Prévision temporelle

Lorsqu'une séparation chronologique a été utilisée, les performances des modèles complexes ont fortement diminué.

La baseline naïve, qui utilise la consommation observée 10 minutes auparavant, a obtenu les meilleurs résultats sur la période de test.

Cela montre qu'une approche simple peut être plus adaptée lorsqu'il existe une forte dépendance à court terme dans la série.

## Principaux enseignements

Ce projet m'a permis de comprendre plusieurs points importants :

- un modèle plus complexe n'est pas forcément plus performant ;
- une séparation aléatoire peut donner une vision trop optimiste des performances sur des données temporelles ;
- il est important de respecter l'ordre chronologique lors de l'évaluation d'un modèle de forecasting ;
- les baselines simples sont essentielles pour juger si un modèle complexe apporte réellement une amélioration ;
- les lag features et les moyennes glissantes peuvent être utiles pour intégrer l'historique d'une série temporelle.

## Technologies utilisées

- Python
- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- Google Colab

## Modèles utilisés

- Linear Regression
- Random Forest Regressor
- Gradient Boosting Regressor
- Baseline naïve de persistance

## Métriques d'évaluation

Les modèles ont été évalués avec :

- MAE — Mean Absolute Error
- RMSE — Root Mean Squared Error
- R² — coefficient de détermination

## Structure du projet

~~~text
energy-consumption-data-science/
│
├── README.md
├── requirements.txt
│
├── notebooks/
│   └── 01_eda.ipynb
│
├── data/
│   └── energydata_complete.csv
│
└── models/
    └── best_random_forest.pkl
~~~

## Conclusion

Ce projet m'a permis de suivre différentes étapes d'un projet de Data Science, depuis l'exploration des données jusqu'à l'évaluation des modèles.

Dans un premier temps, les résultats obtenus avec une séparation aléatoire semblaient encourageants, notamment avec le Random Forest. Cependant, la validation temporelle a montré que ces performances ne se maintenaient pas lorsqu'on cherchait réellement à prévoir des périodes futures.

La comparaison avec une baseline naïve m'a également permis de comprendre qu'un modèle simple peut parfois être plus efficace qu'un modèle plus complexe.

Ce projet m'a donc surtout permis de mieux comprendre l'importance du choix de la méthode de validation, de la création de variables temporelles et de l'analyse critique des résultats.
