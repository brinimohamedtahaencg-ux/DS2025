Rapport sur le jeu de données “Adult” (Census Income Dataset)

Introduction

L’analyse de données occupe aujourd’hui une place essentielle dans les domaines de l’économie, des politiques publiques et de l’intelligence artificielle. Parmi les jeux de données les plus utilisés pour l’apprentissage automatique figure le “Adult Dataset”, aussi connu sous le nom de Census Income Dataset. Ce jeu de données, extrait du recensement américain de 1994, est couramment exploité dans les projets de classification supervisée. Il permet notamment de prédire si un individu gagne plus ou moins de 50 000 dollars par an en fonction de ses caractéristiques démographiques et socio-économiques.

L’objectif de ce rapport est de présenter ce jeu de données, d’en expliquer la structure, d’en analyser les caractéristiques principales et de mettre en évidence son intérêt dans le domaine du machine learning.

Développement
1. Origine et contexte

Le Adult Dataset provient du Census Bureau des États-Unis et a été rendu public par l’UCI Machine Learning Repository, une base de données de référence pour les chercheurs et étudiants en intelligence artificielle. Il a été conçu à des fins de recherche, afin d’étudier les corrélations entre les facteurs socio-économiques et le niveau de revenu d’un individu.

Ce jeu de données illustre parfaitement les problématiques réelles liées à la classification, telles que la gestion des données manquantes, le déséquilibre des classes et la présence de variables qualitatives.

2. Structure du jeu de données

Le dataset contient environ 48 842 observations réparties sur 14 variables explicatives et une variable cible (income).
Chaque observation correspond à une personne recensée, et chaque variable décrit un aspect particulier de sa situation personnelle ou professionnelle.

Les principales variables sont :

Age : âge de l’individu (numérique).

Workclass : type d’emploi (ex. Private, Self-emp, Government).

Education et Education-num : niveau d’éducation, sous forme textuelle et numérique.

Marital-status : statut marital (célibataire, marié, etc.).

Occupation : profession exercée.

Relationship : position dans le foyer (époux, enfant, etc.).

Race et Sex : caractéristiques démographiques.

Capital-gain et Capital-loss : gains ou pertes en capital.

Hours-per-week : nombre d’heures travaillées par semaine.

Native-country : pays d’origine.

Income : variable cible, indiquant si le revenu annuel est supérieur ou inférieur à 50 000 dollars.

Cette structure permet d’étudier les interactions entre les différentes caractéristiques et la variable cible, dans le but de construire des modèles prédictifs.

3. Objectifs et applications

L’objectif principal de ce dataset est de prédire la catégorie de revenu (<=50K ou >50K).
Il s’agit donc d’un problème de classification binaire, très utilisé dans les cours et projets d’apprentissage supervisé.

Les applications typiques sont :

la construction de modèles de prédiction à l’aide d’algorithmes tels que la régression logistique, les arbres de décision ou les réseaux de neurones ;

l’analyse de corrélation entre les variables (par exemple, le niveau d’éducation ou le nombre d’heures travaillées) et le revenu ;

l’étude des biais algorithmiques, notamment liés au sexe ou à l’origine, un sujet crucial dans l’éthique de l’intelligence artificielle.

4. Intérêt et limites

Le Adult Dataset présente plusieurs avantages. Il est complet, facile à comprendre et adapté à des expérimentations rapides. Grâce à sa combinaison de variables numériques et catégorielles, il offre une base solide pour apprendre le prétraitement des données et la construction de modèles de machine learning.

Cependant, il présente aussi des limites :

certaines données sont manquantes ou imprécises (notées “?”) ;

le dataset est ancien (1994), ce qui peut limiter sa pertinence dans des contextes actuels ;

il peut révéler ou amplifier des biais sociaux (par exemple, des différences salariales selon le sexe ou l’origine ethnique).

Conclusion

En somme, le Adult Dataset constitue un outil pédagogique et scientifique majeur dans le domaine de l’apprentissage automatique. Il permet non seulement d’expérimenter des techniques de classification supervisée, mais aussi de sensibiliser aux enjeux éthiques liés à l’analyse de données humaines.
Malgré certaines limites liées à son ancienneté et à la qualité de certaines données, il demeure un exemple incontournable pour comprendre comment les algorithmes peuvent exploiter des informations démographiques afin de prédire un résultat socio-économique.
