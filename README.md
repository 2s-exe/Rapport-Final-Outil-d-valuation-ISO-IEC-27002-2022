# Rapport Final – Outil d'Évaluation ISO/IEC 27002:2022

**Projet :** WECODE SN3 – Piscine Spécialisation GRC

**Date :** 17 Septembre 2025

## 1. Introduction et Objectifs du Projet

L'objectif principal de ce projet était de concevoir un **outil d'évaluation automatisé sous Excel** basé sur l'Annexe A de la norme **ISO/IEC 27002:2022**. Cet outil sert à mesurer le niveau de **maturité** d'un Système de Management de la Sécurité de l'Information (SMSI), à identifier les lacunes (faiblesses) et à orienter les plans d'amélioration.

L'outil intègre l'ensemble des 93 contrôles de la norme, structurés selon les quatre nouvelles catégories.

---

## 2. Step 0 : Maîtrise des Fonctions Excel Clés

La construction d'un outil de GRC robuste nécessite la maîtrise des fonctions suivantes, comme demandé :

| Fonction Excel | Rôle dans l'Outil GRC |
| :--- | :--- |
| **`AVERAGEIF` / `MOYENNE.SI`** | Calcul du **Score Moyen par Catégorie** en ignorant les contrôles non-applicables (`"N"`). Essentiel pour la précision. |
| **`XLOOKUP` / `RECHERCHEX`** | **Robustesse et flexibilité.** Utilisé dans la feuille `Summary` pour convertir le score de maturité numérique (ex. : 3) en texte (ex. : "Quantitatively Managed"). |
| **`FLOOR.MATH` / `ARRONDI.INF`** | Calcul du **Niveau de Maturité** (entier 0-5) en arrondissant le score moyen à l'unité inférieure. |
| **`COUNTIF` / `NB.SI`** | Utilisé pour générer la source de données pour le graphique d'applicabilité, comptant les contrôles marqués `Y` ou `N`. |
| **Références Absolues ($A$1)** | Assurer la **fiabilité des formules** (ex. : la référence au score maximal de 5) lors de la copie de formules, évitant les erreurs. |

---

## 3. Step 1 & 2 : Structure, Contenu et Formules de Calcul

### A. Structure des Contrôles ISO/IEC 27002:2022

L'évaluation est structurée autour des 4 nouvelles catégories de la norme :

1.  **Organizational Controls (5.01-5.37) :** 37 Contrôles
2.  **People Controls (6.01-6.08) :** 8 Contrôles
3.  **Physical Controls (7.01-7.14) :** 14 Contrôles
4.  **Technological Controls (8.01-8.34) :** 34 Contrôles

### B. Structure des Feuilles de Catégorie

Chaque feuille d'évaluation (Catégories 5 à 8) utilise une structure uniforme garantissant la traçabilité des données. Les colonnes clés sont : `ID`, `Nom du Contrôle`, `Applicable (Y/N)`, `Point of Contact`, `Implémenté (0-5)`, `Réponses`, `Evidence`, `Commentaires`.

### C. Logique et Formules de Notation

| Élément du Calcul | Formule Excel Recommandée | Logique et Justification |
| :--- | :--- | :--- |
| **Score par Contrôle** | `=AVERAGE(G15:G18)` | Moyenne directe des 4 questions (2 ouvertes, 2 fermées). Une approche simple et équilibrée. |
| **Score par Catégorie** | `=AVERAGEIF(B:B,"Y",I:I)` | Utilise `AVERAGEIF` pour ne moyenner que les scores des contrôles où la colonne `Applicable` (`B:B`) contient `"Y"`, assurant la pertinence du périmètre. |
| **Maturité (Entier)** | `=FLOOR.MATH(Score_Moyen, 1)` | Détermine le niveau de maturité entier (0-5). Un score de 3.99 est arrondi à **3** (Quantitatively Managed). |

---

## 4. Step 3 : Synthèse et Visualisation

La feuille **`Summary`** est le tableau de bord de l'outil, offrant une synthèse des résultats et des outils de visualisation cruciaux.

### A. Tableau de Synthèse Global

Le score global du SMSI est la moyenne des scores des quatre catégories :
$$\text{Score Global} = \frac{(3.66 + 3.84 + 3.95 + 3.73)}{4} = 3.795$$

| Score Global (3.795) | Niveau de Maturité (3) | Signification Textuelle |
| :--- | :--- | :--- |
| **Overall Score** | **Overall Maturity Level** | **Textual Meaning** |
| 3.795 | 3 | Quantitatively Managed |

### B. Logique des Graphiques de Visualisation

Les graphiques sont choisis pour leur impact sur l'interprétation.

| Graphique | Objectif de l'Interprétation | Données Sources |
| :--- | :--- | :--- |
| **Bar Chart (Applicabilité)** | **Validation du périmètre (Scope).** | Compteur `COUNTIF` des contrôles `Y` et `N` par catégorie. |
| **Spider Chart (Radar)** | **Identification des Faiblesses Relatives.** | Score d'implémentation (0-5) par catégorie. Permet de voir si le SMSI est harmonieux (cercle) ou déséquilibré (pics et creux). **Faiblesse : Catégorie 5 (Organisationnels) à 3.66.** |
| **Bar Chart (Scores)** | **Comparaison Absolue et Priorisation.** | Score d'implémentation (0-5) par catégorie. Aide à classer les domaines : **Force : Catégorie 7 (Physiques) à 3.95.** |

---

## Annexe – Exemple Concret d'Évaluation (Contrôle 5.01)

| ID | Contrôle | Applicabilité | Point of Contact | Score (0–5) | Interprétation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 5.01 | Policies for information security | Y | ISO / Direction | 3 | Le score de 3/5 correspond à un niveau **Managed (Défini)**. La politique existe, mais sa revue annuelle n'est pas systématique, ce qui indique un processus défini mais non encore entièrement mesuré et appliqué. |

---

## Conclusion

L'outil Excel est désormais complet. Il fournit une structure robuste pour :
1.  **Vérifier l'Applicabilité** des 93 contrôles de l'ISO 27002:2022.
2.  **Évaluer l'Implémentation** via une notation quantitative (0-5).
3.  **Justifier** chaque décision et centraliser les preuves.
4.  **Générer automatiquement** un niveau de maturité global.

L'entreprise peut ainsi transformer le score global de **3.795 (Niveau 3 : Quantitatively Managed)** en actions d'amélioration ciblées, en priorisant notamment les Contrôles Organisationnels (Catégorie 5).



                                                 Fait par : SOW SAIDOU
