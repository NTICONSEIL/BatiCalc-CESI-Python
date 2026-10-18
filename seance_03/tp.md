# BatiCalc — TP étudiant — Mission 03 : structurer l'application

**Durée :** 4 h, cours inclus. **Livrable :** `bati_calc_s3.py` et fiche de tests.

## Contexte

Le devis S2 fonctionne, mais ses trois listes parallèles sont fragiles. Le responsable informatique de BÂTI33 demande une structure unique par poste et des calculs réutilisables.

## Étape A — Diagnostic (10 min)

Expliquer ce qui se passe si un matériau est ajouté à `designations` mais pas à `prix_unitaires`. Identifier au moins deux risques de maintenance.

## Étape B — Dictionnaire chantier (20 min)

Créer `chantier` avec référence CH-2026-001, longueur 6, largeur 4, hauteur 2,5, porte 2,4 × 2,1, dalle 0,15. Afficher les valeurs par leurs clés.

## Étape C — Liste de dictionnaires (25 min)

Transformer les trois postes de S2 en une liste `postes` de dictionnaires, chacun contenant `designation`, `quantite`, `prix_unitaire` et `unite`. Parcourir cette liste pour afficher les postes.

## Étape D — Fonctions géométriques (25 min)

Créer `calculer_surface_murs(chantier)`, `calculer_volume_beton(chantier)` et `calculer_parpaings(surface_nette, taux_pertes)`. Réutiliser les formules de S1. Contrôler les résultats avec le chantier de référence.

## Étape E — Fonctions de devis (25 min)

Créer `calculer_montant(poste)`, `calculer_total(postes)` et `afficher_devis(postes)`. Éviter de refaire le même calcul dans plusieurs endroits du programme.

## Étape F — Mise à jour automatique (20 min)

Construire les quantités des postes « Parpaings » et « Béton » à partir des fonctions géométriques, sans saisir manuellement 473 et 3,6. La main-d'œuvre reste un forfait de 40 h.

## Étape G — Recette (15 min)

| Test | Attendu |
|---|---|
| T1 : surface nette | 44,96 m² |
| T2 : parpaings | 473 |
| T3 : béton | 3,60 m³ |
| T4 : devis initial | 3 053,40 € HT |
| T5 : ajout transport 120 € | 3 173,40 € HT |

## Critères de réussite

Les données sont structurées en dictionnaires, les postes en liste de dictionnaires, les fonctions de calcul renvoient leurs résultats, les résultats métier sont conservés et le code ne dépend d'aucune bibliothèque externe hormis la bibliothèque standard.

**Défis facultatifs :** rechercher un poste par nom ; ajouter une fonction de validation du chantier ; séparer calculs et affichage.

**À remettre :** programme exécutable, cinq résultats de tests et une explication de la différence entre `return` et `print`.
