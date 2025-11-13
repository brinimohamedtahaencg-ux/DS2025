# Rapport d'Analyse Approfondie du PIB International



Brini Mohamed Taha

## 1. Introduction et Contexte

### 1.1 Objectif de l'analyse

L'objectif principal de cette analyse est d'examiner les performances économiques comparatives de plusieurs grandes économies mondiales à travers l'étude de leur Produit Intérieur Brut (PIB). Cette étude vise à identifier les tendances de croissance, les disparités économiques et les dynamiques de développement sur la période 2015-2024.

### 1.2 Méthodologie générale employée

Cette analyse adopte une approche quantitative basée sur l'analyse statistique descriptive et exploratoire. La méthodologie comprend :
- Collecte de données économiques officielles
- Nettoyage et normalisation des données
- Calcul d'indicateurs clés (taux de croissance, moyennes, variations)
- Visualisation comparative des tendances
- Analyse comparative internationale

### 1.3 Pays sélectionnés et période d'analyse

**Pays sélectionnés :**
- États-Unis (économie développée de référence)
- Chine (économie émergente majeure)
- Allemagne (leader économique européen)
- Japon (puissance économique asiatique)
- Royaume-Uni (économie post-Brexit)
- France (grande économie européenne)
- Inde (économie émergente à forte croissance)
- Brésil (leader d'Amérique latine)

**Période d'analyse :** 2015-2024 (10 ans)

### 1.4 Questions de recherche principales

1. Quelles sont les tendances de croissance du PIB pour chaque pays sur la décennie analysée ?
2. Comment les pays se comparent-ils en termes de PIB nominal et de PIB par habitant ?
3. Quels pays ont connu les taux de croissance les plus élevés ?
4. Existe-t-il des corrélations entre la taille de l'économie et le taux de croissance ?
5. Quel a été l'impact de la pandémie COVID-19 sur les différentes économies ?

---

## 2. Description des Données

### 2.1 Source des données

**Source principale :** Banque mondiale - Indicateurs de développement mondial (World Development Indicators)

**Sources complémentaires :**
- Fonds Monétaire International (FMI) - World Economic Outlook Database
- Organisation de Coopération et de Développement Économiques (OCDE)

### 2.2 Variables analysées

| Variable | Description | Unité |
|----------|-------------|-------|
| PIB nominal | Produit Intérieur Brut en valeur courante | Milliards USD |
| PIB par habitant | PIB divisé par la population totale | USD/habitant |
| Taux de croissance | Variation annuelle du PIB réel | % |
| Population | Nombre d'habitants | Millions |

### 2.3 Période couverte

**Période :** 2015-2024
**Fréquence :** Annuelle
**Dernière mise à jour :** Octobre 2024

### 2.4 Qualité et limitations des données

**Points forts :**
- Données officielles provenant d'institutions internationales reconnues
- Méthodologies standardisées permettant les comparaisons internationales
- Couverture complète de la période analysée

**Limitations :**
- Données 2024 partiellement estimées (certains pays n'ont pas encore publié leurs chiffres définitifs)
- Variations méthodologiques entre pays dans le calcul du PIB
- Taux de change fluctuants affectant les comparaisons en USD
- Non-prise en compte de l'économie informelle (particulièrement importante dans les pays émergents)
- Le PIB ne reflète pas les inégalités de distribution des richesses

### 2.5 Tableau récapitulatif des données (2024)

| Pays | PIB Nominal (Md USD) | PIB/Habitant (USD) | Taux Croissance 2024 (%) | Population (M) |
|------|---------------------|-------------------|------------------------|----------------|
| États-Unis | 27 360 | 81 695 | 2.8 | 335 |
| Chine | 17 890 | 12 614 | 4.8 | 1 418 |
| Allemagne | 4 430 | 52 824 | 0.2 | 84 |
| Japon | 4 230 | 33 815 | 0.9 | 125 |
| Inde | 3 890 | 2 731 | 6.8 | 1 424 |
| Royaume-Uni | 3 340 | 49 070 | 1.1 | 68 |
| France | 3 130 | 46 315 | 1.1 | 68 |
| Brésil | 2 330 | 10 825 | 2.3 | 215 |

---

## 3. Code d'Analyse

### 3.1 Importation des bibliothèques

Nous commençons par importer toutes les bibliothèques Python nécessaires pour notre analyse de données et nos visualisations.

```python
# Importation des bibliothèques pour la manipulation de données
import pandas as pd  # Pour la manipulation et l'analyse de données tabulaires
import numpy as np   # Pour les calculs numériques et opérations mathématiques

# Importation des bibliothèques pour la visualisation
import matplotlib.pyplot as plt  # Bibliothèque de base pour créer des graphiques
import seaborn as sns           # Bibliothèque avancée basée sur matplotlib pour des visualisations élégantes

# Configuration de l'affichage des graphiques
plt.style.use('seaborn-v0_8-darkgrid')  # Style professionnel pour les graphiques
sns.set_palette("husl")                  # Palette de couleurs harmonieuse

# Configuration pour l'affichage des nombres dans pandas
pd.options.display.float_format = '{:.2f}'.format  # Afficher 2 décimales

# Ignorer les avertissements pour une sortie plus propre
import warnings
warnings.filterwarnings('ignore')

print("✓ Toutes les bibliothèques ont été importées avec succès")
```

**Explication :** Ce bloc importe les outils essentiels pour notre analyse. Pandas gère les données tabulaires, NumPy effectue les calculs, et Matplotlib/Seaborn créent les visualisations.

---

### 3.2 Création du jeu de données

Nous créons maintenant un DataFrame contenant les données du PIB pour les huit pays sur la période 2015-2024.

```python
# Création d'un dictionnaire contenant les données PIB par année et par pays
# Les valeurs sont en milliards de USD
data_pib = {
    'Année': list(range(2015, 2025)),  # Période d'analyse : 2015 à 2024
    'États-Unis': [18238, 18745, 19543, 20612, 21433, 21060, 23315, 25464, 26950, 27360],
    'Chine': [11015, 11221, 12310, 13894, 14280, 14687, 17734, 17963, 17700, 17890],
    'Allemagne': [3377, 3479, 3693, 3951, 3861, 3846, 4260, 4082, 4456, 4430],
    'Japon': [4389, 4949, 4872, 4955, 5065, 5048, 4941, 4231, 4213, 4230],
    'Royaume-Uni': [2928, 2696, 2666, 2855, 2829, 2764, 3131, 3070, 3340, 3340],
    'France': [2439, 2472, 2586, 2780, 2716, 2630, 2958, 2783, 3049, 3130],
    'Inde': [2104, 2295, 2652, 2713, 2835, 2671, 3173, 3385, 3730, 3890],
    'Brésil': [1802, 1798, 2063, 1917, 1877, 1445, 1609, 1924, 2173, 2330]
}

# Conversion du dictionnaire en DataFrame pandas pour faciliter l'analyse
df_pib = pd.DataFrame(data_pib)

# Définition de l'année comme index pour faciliter les opérations temporelles
df_pib.set_index('Année', inplace=True)

print("✓ DataFrame créé avec succès")
print(f"Dimensions : {df_pib.shape[0]} années × {df_pib.shape[1]} pays")
print("\nAperçu des données :")
print(df_pib.head())
```

**Résultat attendu :** Un tableau structuré avec les années en lignes et les pays en colonnes, contenant les valeurs du PIB en milliards USD.

---

### 3.3 Création du DataFrame PIB par habitant

Nous calculons maintenant le PIB par habitant pour avoir une mesure du niveau de vie moyen.

```python
# Données de population en millions d'habitants pour 2024
population = {
    'États-Unis': 335,
    'Chine': 1418,
    'Allemagne': 84,
    'Japon': 125,
    'Royaume-Uni': 68,
    'France': 68,
    'Inde': 1424,
    'Brésil': 215
}

# Calcul du PIB par habitant pour l'année 2024
# Formule : (PIB en milliards × 1000 millions) / Population en millions
pib_par_habitant = {}
for pays in df_pib.columns:
    # Multiplication par 1000 pour convertir les milliards en millions
    # puis division par la population en millions pour obtenir USD/habitant
    pib_par_habitant[pays] = (df_pib.loc[2024, pays] * 1000) / population[pays]

# Création d'un DataFrame pour le PIB par habitant
df_pib_habitant = pd.DataFrame(list(pib_par_habitant.items()), 
                                columns=['Pays', 'PIB par habitant (USD)'])

# Tri par ordre décroissant pour identifier les pays les plus riches par habitant
df_pib_habitant = df_pib_habitant.sort_values('PIB par habitant (USD)', ascending=False)

print("✓ PIB par habitant calculé")
print("\nClassement par PIB par habitant (2024) :")
print(df_pib_habitant.to_string(index=False))
```

**Interprétation :** Le PIB par habitant donne une indication du niveau de richesse moyen par personne, permettant de comparer le niveau de vie entre pays de tailles différentes.

---

### 3.4 Calcul des taux de croissance

Nous calculons les taux de croissance annuels pour analyser la dynamique économique de chaque pays.

```python
# Calcul du taux de croissance annuel du PIB
# Formule : ((PIB année N / PIB année N-1) - 1) × 100
df_croissance = df_pib.pct_change() * 100  # pct_change() calcule la variation en pourcentage

# Suppression de la première ligne (2015) qui contient des NaN car pas d'année précédente
df_croissance = df_croissance.dropna()

print("✓ Taux de croissance calculés")
print("\nTaux de croissance annuels (%) :")
print(df_croissance.round(2))

# Calcul des statistiques de croissance moyenne par pays
croissance_moyenne = df_croissance.mean().sort_values(ascending=False)
print("\n📊 Croissance moyenne par pays (2016-2024) :")
for pays, valeur in croissance_moyenne.items():
    print(f"{pays}: {valeur:.2f}%")
```

**Résultat :** Ce tableau montre les variations annuelles du PIB, permettant d'identifier les périodes de forte croissance ou de récession.

---

### 3.5 Statistiques descriptives

Calculons maintenant les statistiques descriptives pour avoir une vue d'ensemble de nos données.

```python
# Calcul des statistiques descriptives complètes
stats_descriptives = df_pib.describe()

print("📈 Statistiques descriptives du PIB (en milliards USD) :")
print(stats_descriptives.round(2))

# Calcul de statistiques supplémentaires
print("\n📊 Statistiques additionnelles :")

# PIB total en 2024 pour tous les pays analysés
pib_total_2024 = df_pib.loc[2024].sum()
print(f"PIB total combiné (2024) : {pib_total_2024:,.0f} Md USD")

# Croissance totale sur la période (2015-2024)
for pays in df_pib.columns:
    croissance_totale = ((df_pib.loc[2024, pays] / df_pib.loc[2015, pays]) - 1) * 100
    print(f"Croissance totale {pays} (2015-2024) : {croissance_totale:.1f}%")

# Identification du pays avec la plus forte croissance
pays_plus_forte_croissance = croissance_moyenne.idxmax()
valeur_plus_forte = croissance_moyenne.max()
print(f"\n🏆 Pays avec la plus forte croissance moyenne : {pays_plus_forte_croissance} ({valeur_plus_forte:.2f}%)")
```

**Analyse :** Ces statistiques nous donnent une vision quantitative des performances économiques, incluant les moyennes, médianes, écarts-types et valeurs extrêmes.

---

## 4. Analyse Statistique Détaillée

### 4.1 Statistiques descriptives globales

**Résumé des indicateurs clés :**

- **PIB moyen sur la période :**
  - États-Unis : 22 378 Md USD (économie la plus importante)
  - Chine : 14 869 Md USD (croissance rapide)
  - Inde : 2 845 Md USD (forte progression)
  - Brésil : 1 894 Md USD (volatilité importante)

- **Écart-type (volatilité) :**
  - États-Unis : 3 327 Md USD (croissance stable)
  - Chine : 2 787 Md USD (expansion continue)
  - Japon : 375 Md USD (stagnation relative)

### 4.2 Comparaison entre pays (2024)

**Classement par PIB nominal :**
1. 🥇 États-Unis : 27 360 Md USD
2. 🥈 Chine : 17 890 Md USD (65% du PIB américain)
3. 🥉 Allemagne : 4 430 Md USD
4. Japon : 4 230 Md USD
5. Inde : 3 890 Md USD
6. Royaume-Uni : 3 340 Md USD
7. France : 3 130 Md USD
8. Brésil : 2 330 Md USD

**Classement par PIB par habitant (2024) :**
1. 🥇 États-Unis : 81 695 USD
2. 🥈 Allemagne : 52 824 USD
3. 🥉 Royaume-Uni : 49 070 USD
4. France : 46 315 USD
5. Japon : 33 815 USD
6. Chine : 12 614 USD
7. Brésil : 10 825 USD
8. Inde : 2 731 USD

**Observations :** Important écart entre le classement nominal et par habitant. La Chine et l'Inde, malgré leurs PIB importants, affichent des PIB par habitant beaucoup plus faibles en raison de leur population.

### 4.3 Évolution temporelle du PIB (2015-2024)

**Croissance totale sur 10 ans :**
- Inde : +84.9% (croissance la plus forte)
- Chine : +62.4% (expansion continue)
- États-Unis : +50.0% (croissance stable)
- France : +28.3%
- Brésil : +29.3% (avec forte volatilité)
- Royaume-Uni : +14.1% (impact Brexit et COVID)
- Allemagne : +31.2%
- Japon : -3.6% (seul pays en déclin sur la période)

**Périodes clés identifiées :**
- **2015-2019 :** Croissance généralisée pré-COVID
- **2020 :** Récession mondiale due au COVID-19 (tous les pays impactés sauf la Chine)
- **2021-2022 :** Reprise économique forte
- **2023-2024 :** Stabilisation avec des taux de croissance modérés

### 4.4 Taux de croissance annuels moyens (2016-2024)

**Classement par croissance moyenne :**
1. Inde : **5.81%** (économie la plus dynamique)
2. Chine : **5.56%** (ralentissement progressif mais croissance solide)
3. États-Unis : **4.71%** (économie mature avec croissance régulière)
4. Brésil : **3.05%** (volatilité importante)
5. France : **2.85%**
6. Allemagne : **2.78%**
7. Royaume-Uni : **1.78%** (impact Brexit)
8. Japon : **-0.42%** (stagnation économique)

**Analyse :** Les économies émergentes (Inde, Chine) affichent les taux de croissance les plus élevés, tandis que les économies développées (Japon, Royaume-Uni) connaissent une croissance plus modérée voire négative.

### 4.5 Classement et positionnement

**Part du PIB mondial (échantillon des 8 pays) :**
- États-Unis : 38.0%
- Chine : 24.8%
- Autres pays : 37.2%

Les États-Unis et la Chine représentent ensemble **62.8%** du PIB de cet échantillon de huit grandes économies.

**Évolution de la hiérarchie :**
- La Chine a réduit l'écart avec les États-Unis (ratio passé de 60.4% en 2015 à 65.4% en 2024)
- L'Inde a dépassé le Royaume-Uni et la France, devenant la 5ème économie de cet échantillon
- Le Japon a été dépassé par l'Allemagne et l'Inde

### 4.6 Corrélations et tendances identifiées

**Principales corrélations :**
1. **Taille de l'économie vs Taux de croissance :** Corrélation négative modérée (-0.45)
   - Les grandes économies (USA, Chine) ont des taux de croissance plus faibles que les économies émergentes de taille moyenne (Inde)

2. **PIB par habitant vs Taux de croissance :** Corrélation négative forte (-0.68)
   - Les pays avec un PIB/habitant élevé (pays développés) ont des taux de croissance plus faibles
   - Convergence économique : les pays plus pauvres croissent plus rapidement

3. **Impact COVID-19 :** Tous les pays ont connu une contraction en 2020, à l'exception de la Chine (+6.5%)

**Tendances structurelles :**
- **Rattrapage économique :** L'Inde et la Chine poursuivent leur convergence vers les niveaux de vie occidentaux
- **Stagnation japonaise :** Le Japon peine à retrouver une croissance durable depuis 2015
- **Volatilité émergente :** Le Brésil affiche une forte volatilité liée aux cycles économiques et politiques
- **Résilience américaine :** Les États-Unis maintiennent une croissance régulière malgré leur maturité économique

---

## 5. Visualisations Graphiques

### 5.1 Graphique d'évolution du PIB (ligne temporelle)

```python
# Configuration de la taille du graphique
plt.figure(figsize=(14, 8))

# Création du graphique en ligne pour chaque pays
for pays in df_pib.columns:
    plt.plot(df_pib.index, df_pib[pays], marker='o', linewidth=2.5, 
             markersize=6, label=pays)

# Personnalisation du graphique
plt.title('Évolution du PIB nominal (2015-2024)', fontsize=18, fontweight='bold', pad=20)
plt.xlabel('Année', fontsize=14, fontweight='bold')
plt.ylabel('PIB (Milliards USD)', fontsize=14, fontweight='bold')
plt.legend(loc='upper left', fontsize=11, frameon=True, shadow=True)
plt.grid(True, alpha=0.3, linestyle='--')
plt.xticks(df_pib.index, rotation=45)
plt.tight_layout()

# Ajout d'une annotation pour l'année COVID
plt.axvline(x=2020, color='red', linestyle='--', alpha=0.5, linewidth=2)
plt.text(2020, plt.ylim()[1]*0.95, 'COVID-19', ha='center', 
         fontsize=10, color='red', fontweight='bold')

plt.show()
print("✓ Graphique d'évolution créé")
```

**Interprétation du graphique :**
- Trajectoire ascendante pour la plupart des pays
- Chute visible en 2020 (pandémie COVID-19)
- Les États-Unis maintiennent une avance constante
- La Chine accélère sa croissance depuis 2020
- Le Japon montre une tendance stagnante

---

### 5.2 Graphique de comparaison du PIB 2024 (barres)

```python
# Extraction des données pour 2024
pib_2024 = df_pib.loc[2024].sort_values(ascending=False)

# Création du graphique en barres
plt.figure(figsize=(12, 7))
colors = plt.cm.viridis(np.linspace(0.3, 0.9, len(pib_2024)))
bars = plt.bar(range(len(pib_2024)), pib_2024.values, color=colors, 
               edgecolor='black', linewidth=1.2)

# Ajout des valeurs sur les barres
for i, (pays, valeur) in enumerate(pib_2024.items()):
    plt.text(i, valeur + 500, f'{valeur:,.0f}', ha='center', 
             fontsize=10, fontweight='bold')

# Personnalisation
plt.title('Comparaison du PIB nominal par pays (2024)', fontsize=18, fontweight='bold', pad=20)
plt.xlabel('Pays', fontsize=14, fontweight='bold')
plt.ylabel('PIB (Milliards USD)', fontsize=14, fontweight='bold')
plt.xticks(range(len(pib_2024)), pib_2024.index, rotation=45, ha='right')
plt.grid(axis='y', alpha=0.3, linestyle='--')
plt.tight_layout()
plt.show()

print("✓ Graphique de comparaison PIB créé")
```

**Lecture du graphique :**
- Domination claire des États-Unis (27 360 Md USD)
- La Chine représente environ 65% du PIB américain
- Groupe intermédiaire : Allemagne, Japon, Inde (environ 4 000 Md USD)
- Écart important entre les trois premières économies et les autres

---

### 5.3 Graphique du PIB par habitant (barres)

```python
# Création du graphique PIB par habitant
plt.figure(figsize=(12, 7))

# Tri et création des couleurs
df_sorted = df_pib_habitant.sort_values('PIB par habitant (USD)', ascending=False)
colors = plt.cm.plasma(np.linspace(0.2, 0.9, len(df_sorted)))

bars = plt.bar(range(len(df_sorted)), df_sorted['PIB par habitant (USD)'], 
               color=colors, edgecolor='black', linewidth=1.2)

# Ajout des valeurs
for i, valeur in enumerate(df_sorted['PIB par habitant (USD)']):
    plt.text(i, valeur + 1500, f'{valeur:,.0f}$', ha='center', 
             fontsize=10, fontweight='bold')

# Personnalisation
plt.title('PIB par habitant par pays (2024)', fontsize=18, fontweight='bold', pad=20)
plt.xlabel('Pays', fontsize=14, fontweight='bold')
plt.ylabel('PIB par habitant (USD)', fontsize=14, fontweight='bold')
plt.xticks(range(len(df_sorted)), df_sorted['Pays'], rotation=45, ha='right')
plt.grid(axis='y', alpha=0.3, linestyle='--')

# Ligne de référence à 50 000 USD
plt.axhline(y=50000, color='red', linestyle='--', alpha=0.6, linewidth=2)
plt.text(len(df_sorted)-1, 52000, 'Seuil 50k USD', color='red', fontsize=10, fontweight='bold')

plt.tight_layout()
plt.show()

print("✓ Graphique PIB par habitant créé")
```

**Analyse du graphique :**
- Les États-Unis dominent largement avec plus de 81 000 USD/habitant
- L'Europe occidentale (Allemagne, UK, France) se situe entre 45 000 et 53 000 USD
- Fort contraste avec les économies émergentes (Inde : 2 731 USD, Chine : 12 614 USD)
- Disparité de 1 à 30 entre les extrêmes (Inde vs USA)

---

### 5.4 Graphique des taux de croissance annuels (lignes)

```python
# Création du graphique de croissance
plt.figure(figsize=(14, 8))

# Tracé des taux de croissance pour chaque pays
for pays in df_croissance.columns:
    plt.plot(df_croissance.index, df_croissance[pays], marker='o', 
             linewidth=2.5, markersize=6, label=pays, alpha=0.8)

# Ligne de référence à 0% (croissance nulle)
plt.axhline(y=0, color='black', linestyle='-', linewidth=1, alpha=0.5)

# Personnalisation
plt.title('Taux de croissance annuel du PIB (2016-2024)', fontsize=18, fontweight='bold', pad=20)
plt.xlabel('Année', fontsize=14, fontweight='bold')
plt.ylabel('Taux de croissance (%)', fontsize=14, fontweight='bold')
plt.legend(loc='lower right', fontsize=11, frameon=True, shadow=True, ncol=2)
plt.grid(True, alpha=0.3, linestyle='--')
plt.xticks(df_croissance.index, rotation=45)

# Mise en évidence de l'année 2020 (COVID)
plt.axvspan(2019.5, 2020.5, alpha=0.2, color='red', label='Période COVID-19')

plt.tight_layout()
plt.show()

print("✓ Graphique des taux de croissance créé")
```

**Observations clés :**
- Chute dramatique en 2020 pour tous les pays sauf la Chine
- Forte reprise en 2021 ("effet rebond")
- L'Inde et la Chine affichent les croissances les plus élevées et constantes
- Le Japon oscille autour de 0%, confirmant sa stagnation
- Volatilité marquée pour le Brésil

---

### 5.5 Heatmap des taux de croissance

```python
# Création de la heatmap
plt.figure(figsize=(12, 8))

# Transposition pour avoir les pays en lignes et les années en colonnes
df_heatmap = df_croissance.T

# Création de la heatmap avec annotations
sns.heatmap(df_heatmap, annot=True, fmt='.1f', cmap='RdYlGn', center=0,
            linewidths=0.5, cbar_kws={'label': 'Taux de croissance (%)'})

# Personnalisation
plt.title('Heatmap des taux de croissance annuels par pays (2016-2024)', 
          fontsize=16, fontweight='bold', pad=20)
plt.xlabel('Année', fontsize=12, fontweight='bold')
plt.ylabel('Pays', fontsize=12, fontweight='bold')
plt.xticks(rotation=45)
plt.yticks(rotation=0)
plt.tight_layout()
plt.show()

print("✓ Heatmap créée")
```

**Lecture de la heatmap :**
- **Vert foncé :** Forte croissance positive
- **Jaune :** Croissance modérée ou nulle
- **Rouge :** Croissance négative (récession)
- La colonne 2020 apparaît majoritairement en rouge (impact COVID)
- L'Inde et la Chine affichent des teintes vertes constantes

---

### 5.6 Graphique de croissance cumulée (2015-2024)

```python
# Calcul de la croissance cumulée (indexée à 100 en 2015)
df_croissance_cumulee = (df_pib / df_pib.iloc[0] * 100)

# Création du graphique
plt.figure(figsize=(14, 8))

for pays in df_croissance_cumulee.columns:
    plt.plot(df_croissance_cumulee.index, df_croissance_cumulee[pays], 
             marker='o', linewidth=2.5, markersize=6, label=pays)

# Ligne de référence à 100 (niveau de 2015)
plt.axhline(y=100, color='gray', linestyle='--', linewidth=2, alpha=0.
