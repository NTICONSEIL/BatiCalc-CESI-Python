# BatiCalc — TP étudiant — Mission 04 : suivi budgétaire et sauvegarde

**Durée :** 4 h, cours inclus. **Livrables :** `bati_calc.py`, `chantier.json` et fiche de recette.

## Contexte

Le dirigeant de BÂTI33 veut conserver le devis entre deux exécutions et enregistrer les dépenses réelles du chantier CH-2026-001. Votre programme S3 sert de point de départ.

## Données de recette

| Poste | Prévision HT | Réel HT |
|---|---:|---:|
| Parpaings | 851,40 € | 900,00 € |
| Béton | 522,00 € | 540,00 € |
| Main-d'œuvre | 1 680,00 € | 1 890,00 € |
| **Total** | **3 053,40 €** | **3 330,00 €** |

## Travail demandé

### Étape A — Préparer le menu (20 min)

Créer une boucle qui propose les options : afficher le chantier, calculer les matériaux, afficher le devis, saisir les dépenses réelles, afficher le bilan, sauvegarder, charger, quitter. Les options non reconnues doivent être signalées.

### Étape B — Enregistrer les dépenses (25 min)

Ajouter à chaque poste une clé `reel` initialisée à `None` (non renseigné). Permettre à l'utilisateur de saisir un montant réel **positif ou nul**. Gérer les erreurs de conversion avec `try` / `except ValueError`.

### Étape C — Calculer les écarts (20 min)

Pour chaque poste renseigné, afficher le montant prévu, le montant réel et l'écart `réel - prévu`. Calculer le bilan total uniquement lorsque tous les postes disposent d'un montant réel ; sinon signaler que le bilan est incomplet.

### Étape D — Sauvegarder en JSON (20 min)

Enregistrer le dictionnaire `dossier` contenant `chantier` et `postes` dans `chantier.json`. Utiliser `json.dump(..., ensure_ascii=False, indent=2)`.

### Étape E — Charger et gérer les erreurs (25 min)

Lire `chantier.json` avec `json.load`. Intercepter `FileNotFoundError` et `json.JSONDecodeError`. Vérifier au minimum la présence des clés `chantier` et `postes` avant de remplacer les données en mémoire.

### Étape F — Recette finale (30 min)

Exécuter les tests suivants et consigner le résultat :

| Test | Attendu |
|---|---|
| T1 : devis initial | 3 053,40 € HT |
| T2 : dépenses 900 / 540 / 1 890 | Total réel 3 330 € ; écart +276,60 € ; +9,06 % |
| T3 : sauvegarde et chargement | Données identiques |
| T4 : fichier absent | Message clair sans arrêt brutal |
| T5 : saisie `abc` pour une dépense | Saisie redemandée |
| T6 : option `99` | Retour au menu |
| T7 : un poste réel non renseigné | Bilan annoncé incomplet |

## Critères de réussite

Le menu fonctionne jusqu'à « Quitter » ; les calculs sont corrects ; la sauvegarde conserve les données ; les erreurs courantes sont traitées ; les fonctions de S3 sont réutilisées plutôt que dupliquées.

**Défis facultatifs :** afficher les postes triés par dépassement ; produire un fichier de rapport texte ; enregistrer plusieurs chantiers dans des fichiers distincts.

**À remettre :** programme final, fichier JSON généré, tableau des sept tests et trois phrases expliquant les principales difficultés rencontrées.
