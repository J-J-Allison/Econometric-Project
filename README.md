# 🏠 Projet d'Économétrie Appliquée : Analyse des Prix Immobiliers

> **Du modèle linéaire aux méthodes de régularisation**

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)
[![Licence](https://img.shields.io/badge/Licence-Académique-green.svg)](#)

## 📋 Présentation

Ce projet présente une analyse économétrique complète des prix immobiliers à partir d'un jeu de données de 150 transactions réalisées entre 2015 et 2023. Nous appliquons l'ensemble des techniques économétriques — de la régression MCO aux méthodes de régularisation — afin d'identifier et de quantifier les déterminants des prix de l'immobilier.

**Institution :** Université Paris 1 Panthéon-Sorbonne  
**Formation :** DU Sorbonne Data Analytics  
**Cours :** Économétrie Appliquée  
**Date :** Décembre 2025

### 👥 Auteurs

- MANELLI Cédric
- ALLISON Jacques
- NADAT Sufyan

---

## 🎯 Objectifs

1. Identifier les déterminants statistiquement significatifs des prix immobiliers
2. Quantifier la contribution marginale de chaque facteur à la formation des prix
3. Tester la stabilité structurelle du modèle autour de la période COVID-19
4. Traiter les biais d'endogénéité potentiels par variables instrumentales
5. Comparer les performances prédictives des modèles MCO, Ridge et Lasso

---

## 📊 Jeu de Données

| Variable | Description |
|----------|-------------|
| `Surface_m2` | Surface habitable en mètres carrés |
| `Chambres` | Nombre de chambres |
| `Annee_construction` | Année de construction |
| `Distance_centre_km` | Distance au centre-ville (km) |
| `Etage` | Étage (0 = rez-de-chaussée) |
| `Ascenseur` | Présence d'un ascenseur (1 = oui, 0 = non) |
| `Annee_vente` | Année de la vente (2015–2023) |
| `Qualite_ecole` | Score de qualité des écoles du quartier (1–10) |
| `Revenu_median_quartier` | Revenu médian du quartier (k€) |
| `Distance_universite` | Distance à l'université la plus proche (km) |
| `Prix_milliers_euros` | Prix de vente en milliers d'euros (**cible**) |

**Taille de l'échantillon :** 150 observations

---

## 🔬 Méthodologie

### Partie 1 : Analyse Descriptive et Modèles de Base
- Statistiques descriptives et analyse des distributions
- Matrice de corrélation (Pearson)
- Régression linéaire simple (Prix ~ Surface)
- Régression linéaire multiple avec 6 variables explicatives
- Transformations log-linéaire et log-log

### Partie 2 : Diagnostics et Corrections
- Détection de la multicolinéarité (VIF)
- Test d'hétéroscédasticité (Breusch-Pagan)
- Écarts-types robustes de White
- Test d'autocorrélation de Durbin-Watson
- Écarts-types de Newey-West
- Analyse de rupture structurelle (test de Chow, variable Covid)

### Partie 3 : Endogénéité
- Discussion des sources d'endogénéité
- Estimation par Variables Instrumentales (2SLS)
- Instrument : `Distance_universite` pour `Qualite_ecole`
- F-statistique de première étape et tests de validité

### Partie 4 : Régularisation
- Régression Ridge (pénalité L2)
- Régression Lasso (pénalité L1)
- Validation croisée 10-fold pour le choix de λ
- Comparaison train/test (80/20)

---

## 📈 Résultats Principaux

| Métrique | Valeur |
|----------|--------|
| **R² ajusté** | 0,780 |
| **Coefficient Surface** | +4 390 €/m² |
| **Distance au centre** | −6 140 €/km |
| **Effet COVID** | +103 700 € |
| **Prédiction (bien type)** | 2 255 539 € |
| **Intervalle de prévision 95%** | [2 072 207 € – 2 438 871 €] |

### Conclusions Principales

- La **surface** est le prédicteur dominant (r ≈ 0,83 avec le prix)
- **Hétéroscédasticité** détectée → utiliser les écarts-types robustes de White
- **Pas de rupture structurelle** des coefficients (test de Chow), mais déplacement de niveau significatif pendant le COVID
- La **qualité des écoles** présente un biais d'endogénéité positif ; l'estimation IV réduit son effet à la non-significativité
- **Ridge/Lasso** offrent des performances comparables aux MCO sur les données test (RMSE ≈ 92–93)

---

## 🛠️ Technologies

```
pandas          # Manipulation des données
numpy           # Calcul numérique
matplotlib      # Visualisation
seaborn         # Graphiques statistiques
statsmodels     # MCO, tests diagnostiques, estimation IV
scipy           # Tests statistiques
scikit-learn    # Ridge, Lasso, validation croisée, StandardScaler
```

---

## 📁 Structure du Projet

```
├── README.md
├── Rapport_Projet_Econometrie_Appliquee.pdf   # Rapport complet
├── traitement.ipynb                            # Notebook Jupyter avec toutes les analyses
├── donnees_immobilieres.xlsx                   # Jeu de données
└── figures/
    ├── histogrammes.png
    ├── boites_moustaches.png
    ├── matrice_correlation.png
    ├── analyse_residus.png
    ├── coefficients_ridge.png
    ├── coefficients_lasso.png
    └── intervalles_prevision.png
```

---

## 🚀 Démarrage Rapide

### Prérequis

```bash
pip install pandas numpy matplotlib seaborn statsmodels scipy scikit-learn openpyxl
```

### Exécution de l'Analyse

```bash
# Cloner le dépôt
git clone https://github.com/VOTRE_NOM/econometrie-immobilier.git
cd econometrie-immobilier

# Lancer Jupyter
jupyter notebook traitement.ipynb
```

---

## 📖 Résumé du Rapport

L'analyse complète est documentée dans `Rapport_Projet_Econometrie_Appliquee.pdf` (26 pages), couvrant :

1. **Résumé exécutif** – Résultats clés et recommandations
2. **Analyse descriptive** – Distributions des variables, corrélations
3. **Estimation MCO** – Régression simple et multiple, transformations logarithmiques
4. **Diagnostics** – VIF, hétéroscédasticité, autocorrélation, stabilité structurelle
5. **Variables Instrumentales** – Estimation 2SLS pour corriger l'endogénéité
6. **Régularisation** – Ridge & Lasso avec validation croisée
7. **Prévisions** – Estimations ponctuelles et intervalles de confiance

---


## 📜 Licence

Ce projet a été réalisé dans un cadre académique pour le DU Sorbonne Data Analytics de l'Université Paris 1 Panthéon-Sorbonne.

---
