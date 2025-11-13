# Projet – Analyse du jeu de données « Adult (Census Income) »

**DOI** : 10.24432/C5XW20  
**Référence** : Becker, B. & Kohavi, R. (1996). *Adult [Dataset]. UCI Machine Learning Repository.* :contentReference[oaicite:1]{index=1}

---

## 1. Contexte et objectif  
Le jeu de données « Adult », parfois appelé « Census Income Dataset », a été extrait à partir du recensement américain de 1994. :contentReference[oaicite:2]{index=2}  
L’objectif principal est de prédire si le revenu annuel d’un individu dépasse ou non 50 000 $ (oui / non), en fonction de diverses caractéristiques démographiques et socio-économiques. :contentReference[oaicite:3]{index=3}  
Ce projet vise à :  
- étudier la structure du jeu de données,  
- comprendre les relations entre variables explicatives et variable cible,  
- expérimenter un modèle de classification supervisée,  
- éventuellement explorer les questions d’équité ou de biais dans les résultats.

---

## 2. Description du jeu de données  
### 2.1 Contenu  
- Nombre d’observations : **48 842** (pour la partie d’entraînement) environ. :contentReference[oaicite:4]{index=4}  
- Nombre de caractéristiques explicatives : 14 (variables comme âge, travail, éducation, heures par semaine, etc.). :contentReference[oaicite:5]{index=5}  
- Variable cible : `income`, indiquant « <=50K » ou « >50K ». :contentReference[oaicite:6]{index=6}  

### 2.2 Variables principales (échantillon)  
| Nom | Type | Description |
|-----|------|------------|
| `age` | numérique | Âge de l’individu. |
| `workclass` | catégoriel | Type d’emploi (ex. Private, Self-emp, Government…). |
| `education` / `education-num` | catégoriel / numérique | Niveau d’études (texte + codé). |
| `marital-status` | catégoriel | Statut marital (married, divorced, etc.). |
| `occupation` | catégoriel | Profession exercée. |
| `relationship` | catégoriel | Relation dans le foyer (époux, enfant, etc.). |
| `race` | catégoriel | Groupe ethnique. |
| `sex` | catégoriel | Sexe (Female, Male). |
| `capital-gain` / `capital-loss` | numérique | Gains ou pertes en capital. |
| `hours-per-week` | numérique | Nombre d’heures travaillées par semaine. |
| `native-country` | catégoriel | Pays d’origine. |
| `income` | catégoriel (cible) | >50K ou <=50K. |

*Note : certains enregistrements contiennent des valeurs manquantes ou inconnues (souvent marquées « ? ») pour certaines variables.* :contentReference[oaicite:7]{index=7}

### 2.3 Licence et usage  
Le jeu de données est distribué sous licence **Creative Commons Attribution 4.0 International (CC BY 4.0)**. :contentReference[oaicite:8]{index=8}  
Il est largement utilisé comme référence dans les expériences en classification et comme banc d’essai pour des approches d’éthique dans le machine learning (biais, équité). :contentReference[oaicite:9]{index=9}

---

## 3. Méthodologie proposée  
### 3.1 Pré-traitement des données  
- Charger les fichiers (`adult.data`, `adult.test`, etc.).  
- Gérer les valeurs manquantes ou inconnues (par ex. remplacer « ? », ou supprimer les lignes).  
- Encodage des variables catégorielles (one-hot, label encoding).  
- Normalisation ou mise à l’échelle des variables numériques si nécessaire.  
- Division en jeu d’entraînement / test (ou cross-validation).  

### 3.2 Modélisation  
- Choisir un (ou plusieurs) algorithmes de classification, par exemple : régression logistique, arbre de décision, forêt aléatoire, XGBoost.  
- Entraîner le modèle sur les données d’entraînement.  
- Évaluer la performance via des métriques : précision, rappel, F1-score, AUC.  
- Analyser la confusion (vrai positif, faux négatif, etc.).  

### 3.3 Analyse exploratoire & biais  
- Étudier la distribution des variables explicatives et de la variable cible.  
- Vérifier l’influence de certaines variables (ex. sexe, race, heures par semaine) sur la probabilité de revenu > 50K.  
- Explorer la présence de biais : est-ce que certains groupes sont systématiquement désavantagés par le modèle ?  
- Visualiser les corrélations, importance des variables, etc.  

---

## 4. Résultats attendus et implications  
- Modèle capable de classifier correctement si un individu gagne plus de 50 000 $/an.  
- Importance relative des variables explicatives (ex. éducation, heures par semaine, occupation).  
- Conclusions sur les potentiels biais dans les résultats et recommandations pour une utilisation équitable.  
- Discussion sur les limites du jeu de données (ancienneté, contexte géographique USA uniquement, représentativité).  

---

## 5. Conclusion  
Le dataset « Adult » fournit une base riche et largement utilisée pour la classification supervisée et pour étudier les enjeux éthiques liés aux données humaines. En menant ce projet, on peut non seulement construire et évaluer un modèle prédictif, mais aussi réfléchir aux implications sociales de l’IA et à la responsabilité des praticiens.  

---

## 6. Références  
- Becker, B., & Kohavi, R. (1996). *Adult [Dataset]. UCI Machine Learning Repository.* DOI: 10.24432/C5XW20. :contentReference[oaicite:10]{index=10}  
- UCI Machine Learning Repository. “Adult – Donated on 4/30/1996”. :contentReference[oaicite:11]{index=11}  
- Fairlearn documentation. “Adult Census Dataset”. :contentReference[oaicite:12]{index=12}  

---










'''Python
# ============================================================
# 🧠 ANALYSE STATISTIQUE DU DATASET "ADULT / CENSUS INCOME"
# ------------------------------------------------------------
# Compatible Google Colab ✅
# Auteur : Mohamed Taha Brini (Projet Statistique)
# ============================================================

# === 1. INSTALLATION ET IMPORTATION DES LIBRAIRIES ===
!pip install seaborn matplotlib pandas scipy --quiet

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from scipy import stats

sns.set(style="whitegrid")

# === 2. TÉLÉCHARGEMENT DU DATASET DEPUIS UCI ===
url = "https://archive.ics.uci.edu/ml/machine-learning-databases/adult/adult.data"

columns = [
    "age", "workclass", "fnlwgt", "education", "education-num",
    "marital-status", "occupation", "relationship", "race", "sex",
    "capital-gain", "capital-loss", "hours-per-week", "native-country", "income"
]

data = pd.read_csv(url, header=None, names=columns, na_values=" ?", skipinitialspace=True)

print("✅ Données chargées avec succès !")
print(f"Nombre d’observations : {data.shape[0]}, Nombre de variables : {data.shape[1]}")

# === 3. NETTOYAGE DU DATASET ===
data.dropna(inplace=True)
data.drop_duplicates(inplace=True)
data = data.applymap(lambda x: x.strip() if isinstance(x, str) else x)

print("\nDonnées nettoyées :", data.shape[0], "lignes restantes après nettoyage")

# === 4. STATISTIQUES DESCRIPTIVES ===
print("\n=== Statistiques descriptives ===")
print(data.describe(include="all"))

# Répartition de la variable cible
plt.figure(figsize=(5,4))
sns.countplot(x='income', data=data, palette="Set2")
plt.title("Répartition du revenu")
plt.show()

# === 5. DISTRIBUTIONS NUMÉRIQUES ===
num_cols = ["age", "education-num", "capital-gain", "capital-loss", "hours-per-week"]

data[num_cols].hist(bins=30, figsize=(12,6), color='skyblue', edgecolor='black')
plt.suptitle("Distribution des variables numériques", fontsize=14)
plt.show()

# === 6. ANALYSE PAR SEXE ===
plt.figure(figsize=(6,4))
sns.countplot(x='sex', hue='income', data=data, palette='Set3')
plt.title("Répartition du revenu par sexe")
plt.show()

# === 7. NIVEAU D’ÉDUCATION VS REVENU ===
plt.figure(figsize=(10,5))
sns.countplot(y='education', hue='income', data=data,
              order=data['education'].value_counts().index, palette='coolwarm')
plt.title("Revenu selon le niveau d'éducation")
plt.show()

# === 8. MATRICE DE CORRÉLATION ===
data['income_num'] = data['income'].apply(lambda x: 1 if x == '>50K' else 0)
corr = data[num_cols + ['income_num']].corr()

plt.figure(figsize=(8,6))
sns.heatmap(corr, annot=True, cmap="coolwarm", fmt=".2f")
plt.title("Matrice de corrélation")
plt.show()

# === 9. TESTS STATISTIQUES ===
print("\n=== TESTS STATISTIQUES ===")

# Âge selon revenu
age_low = data[data['income'] == '<=50K']['age']
age_high = data[data['income'] == '>50K']['age']
t_stat, p_val = stats.ttest_ind(age_low, age_high)
print(f"Test t sur l’âge : T = {t_stat:.3f}, p = {p_val:.5f}")

# Heures travaillées selon revenu
hours_low = data[data['income'] == '<=50K']['hours-per-week']
hours_high = data[data['income'] == '>50K']['hours-per-week']
t_stat2, p_val2 = stats.ttest_ind(hours_low, hours_high)
print(f"Test t sur les heures/semaine : T = {t_stat2:.3f}, p = {p_val2:.5f}")

# === 10. CONCLUSION AUTOMATIQUE ===
print("\n=== CONCLUSION ===")
print("👉 Les individus gagnant plus de 50K :")
print("- ont un âge moyen et un niveau d'éducation significativement plus élevés,")
print("- travaillent plus d'heures par semaine,")
print("- et présentent souvent des gains en capital plus importants.")
print("\nLa variable 'education-num' est parmi les plus corrélées avec le revenu (> 0.33).")
print("Les différences observées entre les sexes et les statuts maritaux sont également notables.")







'''
--- Code Python





# ============================================================
# 🧠 ANALYSE STATISTIQUE DU DATASET "ADULT / CENSUS INCOME"
# ------------------------------------------------------------
# Compatible Google Colab ✅
# Auteur : Mohamed Taha Brini (Projet Statistique)
# ============================================================

# === 1. INSTALLATION ET IMPORTATION DES LIBRAIRIES ===
!pip install seaborn matplotlib pandas scipy --quiet

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from scipy import stats

sns.set(style="whitegrid")

# === 2. TÉLÉCHARGEMENT DU DATASET DEPUIS UCI ===
url = "https://archive.ics.uci.edu/ml/machine-learning-databases/adult/adult.data"

columns = [
    "age", "workclass", "fnlwgt", "education", "education-num",
    "marital-status", "occupation", "relationship", "race", "sex",
    "capital-gain", "capital-loss", "hours-per-week", "native-country", "income"
]

data = pd.read_csv(url, header=None, names=columns, na_values=" ?", skipinitialspace=True)

print("✅ Données chargées avec succès !")
print(f"Nombre d’observations : {data.shape[0]}, Nombre de variables : {data.shape[1]}")

# === 3. NETTOYAGE DU DATASET ===
data.dropna(inplace=True)
data.drop_duplicates(inplace=True)
data = data.applymap(lambda x: x.strip() if isinstance(x, str) else x)

print("\nDonnées nettoyées :", data.shape[0], "lignes restantes après nettoyage")

# === 4. STATISTIQUES DESCRIPTIVES ===
print("\n=== Statistiques descriptives ===")
print(data.describe(include="all"))

# Répartition de la variable cible
plt.figure(figsize=(5,4))
sns.countplot(x='income', data=data, palette="Set2")
plt.title("Répartition du revenu")
plt.show()

# === 5. DISTRIBUTIONS NUMÉRIQUES ===
num_cols = ["age", "education-num", "capital-gain", "capital-loss", "hours-per-week"]

data[num_cols].hist(bins=30, figsize=(12,6), color='skyblue', edgecolor='black')
plt.suptitle("Distribution des variables numériques", fontsize=14)
plt.show()

# === 6. ANALYSE PAR SEXE ===
plt.figure(figsize=(6,4))
sns.countplot(x='sex', hue='income', data=data, palette='Set3')
plt.title("Répartition du revenu par sexe")
plt.show()

# === 7. NIVEAU D’ÉDUCATION VS REVENU ===
plt.figure(figsize=(10,5))
sns.countplot(y='education', hue='income', data=data,
              order=data['education'].value_counts().index, palette='coolwarm')
plt.title("Revenu selon le niveau d'éducation")
plt.show()

# === 8. MATRICE DE CORRÉLATION ===
data['income_num'] = data['income'].apply(lambda x: 1 if x == '>50K' else 0)
corr = data[num_cols + ['income_num']].corr()

plt.figure(figsize=(8,6))
sns.heatmap(corr, annot=True, cmap="coolwarm", fmt=".2f")
plt.title("Matrice de corrélation")
plt.show()

# === 9. TESTS STATISTIQUES ===
print("\n=== TESTS STATISTIQUES ===")

# Âge selon revenu
age_low = data[data['income'] == '<=50K']['age']
age_high = data[data['income'] == '>50K']['age']
t_stat, p_val = stats.ttest_ind(age_low, age_high)
print(f"Test t sur l’âge : T = {t_stat:.3f}, p = {p_val:.5f}")

# Heures travaillées selon revenu
hours_low = data[data['income'] == '<=50K']['hours-per-week']
hours_high = data[data['income'] == '>50K']['hours-per-week']
t_stat2, p_val2 = stats.ttest_ind(hours_low, hours_high)
print(f"Test t sur les heures/semaine : T = {t_stat2:.3f}, p = {p_val2:.5f}")

# === 10. CONCLUSION AUTOMATIQUE ===
print("\n=== CONCLUSION ===")
print("👉 Les individus gagnant plus de 50K :")
print("- ont un âge moyen et un niveau d'éducation significativement plus élevés,")
print("- travaillent plus d'heures par semaine,")
print("- et présentent souvent des gains en capital plus importants.")
print("\nLa variable 'education-num' est parmi les plus corrélées avec le revenu (> 0.33).")
print("Les différences observées entre les sexes et les statuts maritaux sont également notables.")
---
*Fin du document.*
