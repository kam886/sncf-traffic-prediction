
# Prédiction du nombre de validations en gare SNCF-Transilien

Projet réalisé dans le cadre d’un **data challenge académique** en 2024.

---

## 🎯 Objectif

Anticiper à moyen et long terme le nombre de validations de titres de transport (passages par portiques) dans les gares SNCF-Transilien en Île-de-France.
Ce projet vise à améliorer la performance du service en prévoyant l'affluence quotidienne par gare.

---

## 📂 Données

* `train.csv` : 1 237 971 lignes – validations quotidiennes pour 448 gares du réseau Transilien de janvier 2015 à décembre 2022
* `test.csv` : 78 652 lignes – mêmes gares, de janvier à juin 2023 (à prédire)
* Variables :

  * `date` : date au format YYYY-MM-DD
  * `station` : identifiant anonymisé de la gare
  * `y` : nombre de validations
  * `job` : 1 si jour ouvrable standard, 0 sinon
  * `ferie` : 1 si jour férié
  * `vacances` : 1 si vacances scolaires


**Remarque :** Les données peuvent être téléchargées [https://challengedata.ens.fr/].
---

## Technologies et librairies utilisées

* **Python**
* **Jupyter Notebook**
* `pandas`, `numpy` : manipulation des données
* `matplotlib`, `seaborn` : visualisation
* `scikit-learn` : modèles de régression classiques
* `XGBoost` : boosting performant
* `TensorFlow / Keras` : réseau de neurones (expérimental)

---

## Approche

1. **Exploration des données**

   * Analyse temporelle par station
   * Visualisation des tendances annuelles, mensuelles et hebdomadaires

2. **Feature Engineering**

   * Création de nouvelles variables (jour de la semaine, week-end, etc.)
   * Ajout d’indicateurs contextuels : vacances scolaires, jours fériés, jours ouvrables

3. **Prétraitement des données**

   * Fusion des jeux `X_train` et `Y_train` via une clé combinant la date et la station (`date_station`)
   * Encodage des identifiants de gares avec `LabelEncoder`
   * Nettoyage des dates (suppression des tirets, conversion en chaîne de caractères)
   * Transformation logarithmique de la cible (`log1p(y)`) pour réduire l’impact des valeurs extrêmes

4. **Modélisation**

   * Entraînement de plusieurs modèles sur les données de 2015 à 2022
   * Prédiction sur la période janvier–juin 2023
    

5. **Évaluation**

   * Métrique utilisée : **MAPE** (Mean Absolute Percentage Error)
   * Résultats comparés à un benchmark fourni par le challenge

---

## Modèles testés

* ExtraTreesRegressor
* ExtraTreeRegressor
* LinearRegression
* RidgeRegression
* DecisionTreeRegressor
* RandomForestRegressor
* BaggingRegressor
* GradientBoostingRegressor
* XGBoost
* Réseau de neurones simple (Keras)

---

## Résultats

* Les performances varient selon les modèles et les gares
* XGBoost et RandomForest ont montré les meilleurs résultats en termes de MAPE global
* La transformation logarithmique a amélioré la stabilité des prédictions sur les gares à fort trafic
* Le réseau de neurones a été testé à titre exploratoire et n’a pas surpassé les modèles classiques



