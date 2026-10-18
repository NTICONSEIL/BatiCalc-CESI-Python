# BatiCalc — TP étudiant — Mission 02 : établir un devis

**Durée :** 4 h, cours inclus. **Livrable :** `bati_calc_s2.py` et une fiche de tests.  
**Prérequis :** calculs de la mission 01, `if`, `input`, variables.

## Situation professionnelle

BÂTI33 veut chiffrer le garage CH-2026-001 à partir des quantités calculées dans la mission 01. Le devis contient trois postes : parpaings, béton et main-d'œuvre. Votre mission est de traiter ces postes à l'aide de listes et de boucles.

## Données fournies

| Poste | Quantité | Unité | Prix HT |
|---|---:|---|---:|
| Parpaings | 473 | pièce | 1,80 € |
| Béton | 3,60 | m³ | 145,00 € |
| Main-d'œuvre | 40 | h | 42,00 € |

## Travail demandé

### Étape A — Révision (10 min)

Créer un fichier `bati_calc_s2.py`. Afficher le titre du devis et le numéro de chantier.

### Étape B — Premières listes (15 min)

Créer `designations`, `quantites`, `prix_unitaires`. Afficher le premier et le dernier poste et le nombre de postes. **Question :** pourquoi les indices commencent-ils à 0 ?

### Étape C — Boucle `for` (20 min)

Afficher chaque désignation avec son numéro, puis afficher le montant de chaque ligne. Ne pas dupliquer les instructions de calcul.

### Étape D — Total du devis (25 min)

Initialiser un accumulateur avant la boucle, ajouter chaque montant et afficher le total HT. Comparer au résultat de référence.

### Étape E — Ajouter un poste (20 min)

Ajouter « Transport », quantité 1, prix 120 € à l'aide de `append()` dans chacune des trois listes. Recalculer le total.

### Étape F — `while` et validation (25 min)

Proposer une question « Ajouter un poste ? (o/n) ». Tant que l'utilisateur répond `o`, saisir une désignation, une quantité et un prix positif. Rejeter les valeurs numériques nulles ou négatives. Pour cette séance, on suppose que les nombres saisis sont valides syntaxiquement.

### Étape G — Recette et bilan (15 min)

Tester les cas ci-dessous et noter les résultats.

| Test | Attendu |
|---|---|
| T1 : devis initial | 3 053,40 € |
| T2 : transport à 120 € | 3 173,40 € |
| T3 : prix des parpaings à 3,60 € | 3 904,80 € sans transport |
| T4 : quantité négative lors d'un ajout | Saisie redemandée |
| T5 : réponse `n` | Sortie de la boucle |

## Critères de réussite

- Les trois listes sont synchronisées.
- Chaque poste est affiché par une boucle.
- Le total est calculé par un accumulateur.
- L'utilisateur peut ajouter des postes.
- Les montants sont affichés avec deux décimales.

**Défis facultatifs :** identifier le poste le plus coûteux ; afficher le pourcentage de chaque poste ; détecter les listes de longueurs incohérentes.

**À remettre :** le fichier Python et les résultats des cinq tests. Ne pas utiliser de dictionnaires ou de bibliothèques externes dans la solution obligatoire.
