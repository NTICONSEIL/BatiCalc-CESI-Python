# BatiCalc — TP étudiant — Mission 01

**Durée :** 4 h (dont cours et exercices) · **Livrable :** `bati_calc_s1.py` · **Travail :** individuel ou binôme selon consigne.

## Votre mission
Vous êtes développeur junior chez BÂTI33 Construction. L'entreprise souhaite automatiser une estimation simplifiée des matériaux nécessaires à la construction d'un garage rectangulaire. Vous devez créer un programme Python en ligne de commande.

## Dossier de chantier CH-2026-001
| Paramètre | Valeur |
|---|---:|
| Longueur | 6 m |
| Largeur | 4 m |
| Hauteur des murs | 2,5 m |
| Porte | 2,4 m × 2,1 m |
| Épaisseur de dalle | 0,15 m |
| Surface nominale d'un parpaing | 0,10 m² |
| Pertes et découpes | 5 % |

**Hypothèses :** les quatre murs ont une hauteur constante ; seule l'ouverture de la porte est déduite ; aucun calcul de fondations, toiture, linteaux, chaînages ou mortier. Il s'agit d'un exercice de programmation, pas d'un métré professionnel.

## Étape A — Premier script (10 min)
Créer `bati_calc_s1.py`, afficher le nom de l'entreprise et la référence du chantier. Exécuter le script depuis VS Code.

## Étape B — Variables et calculs simples (20 min)
1. Déclarer `longueur`, `largeur` et `hauteur` avec les valeurs du dossier.
2. Calculer le périmètre, la surface brute des murs et la surface au sol.
3. Afficher chaque résultat avec son unité.
4. Modifier les dimensions et constater les effets.

## Étape C — Saisie utilisateur (20 min)
Remplacer les dimensions fixes par des saisies avec `input()` et `float()`. Afficher les valeurs avec deux décimales. Expliquer pourquoi `input()` doit être converti.

## Étape D — Calcul du béton (20 min)
Calculer le volume de la dalle à partir de la surface au sol et de l'épaisseur de 0,15 m. Afficher le résultat en m³.

## Étape E — Calcul des parpaings (25 min)
1. Déduire la surface de la porte de la surface brute des murs.
2. Diviser la surface nette par 0,10 m² par parpaing.
3. Ajouter 5 % de pertes.
4. Arrondir à l'entier supérieur avec `math.ceil` (`import math`).
5. Afficher le nombre de parpaings.

## Étape F — Conditions de validité (30 min)
Ajouter des tests qui refusent les dimensions nulles ou négatives. Refuser également une surface de porte supérieure ou égale à la surface brute des murs. En cas d'erreur, afficher un message explicite et ne pas afficher d'estimation.

## Étape G — Recette du programme (20 min)
Exécuter les cas suivants et noter « conforme / non conforme » :

| Test | Données | Attendu |
|---|---|---|
| T1 | 6 × 4 × 2,5 m | 44,96 m² nets ; 3,60 m³ ; 473 parpaings |
| T2 | Longueur = 0 | Refus de la saisie |
| T3 | Largeur = -4 | Refus de la saisie |
| T4 | Hauteur = 0 | Refus de la saisie |
| T5 | 1 × 1 × 1 m | Refus : ouverture trop grande |

**Remarque :** la saisie d'un texte à la place d'un nombre n'est pas exigée dans cette séance ; elle sera traitée lors de l'introduction de la gestion d'exceptions.

## Critères de réussite
- Les trois dimensions sont saisies et converties en nombres.
- Les formules et unités sont exactes.
- Le programme calcule 473 parpaings pour le chantier de référence.
- Les valeurs invalides sont refusées sans estimation trompeuse.
- Les noms de variables sont explicites et le code reste lisible.

## Défis facultatifs
1. Afficher le coût des parpaings à 1,80 € pièce.
2. Ajouter un `elif` pour classer le chantier selon la surface au sol : petite (< 20 m²), moyenne (20 à 40 m² inclus), grande (> 40 m²). Ces seuils sont fictifs.
3. Autoriser la saisie des dimensions de la porte, en les contrôlant.

## À remettre
Le fichier `bati_calc_s1.py` et un court tableau des résultats des cinq tests. Le programme doit être exécutable sans dépendance externe.
