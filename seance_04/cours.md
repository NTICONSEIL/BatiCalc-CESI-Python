# BatiCalc — Séance 4 : menus, fichiers JSON et suivi budgétaire

> **CESI — Prépa 1 | Cours étudiant | Mission 04 | 4 h cours et TP compris**  
> **Prérequis :** variables, conditions, boucles, listes, dictionnaires, fonctions.  
> **Objectif métier :** conserver un chantier, enregistrer les dépenses réelles et comparer budget et réalisé.

## Compétences visées

Concevoir un menu interactif, gérer une saisie erronée simple, lire et écrire un fichier JSON, utiliser `try` / `except` pour quelques erreurs courantes, calculer et interpréter un écart budgétaire, effectuer des tests de recette.

## 1. Un programme qui reste actif : menu et boucle

Les versions précédentes se terminaient après l'affichage du devis. Une application console peut proposer plusieurs actions sans redémarrage.

```python
choix = ""
while choix != "0":
    print("1. Afficher le chantier")
    print("2. Afficher le devis")
    print("0. Quitter")
    choix = input("Votre choix : ").strip()
    if choix == "1":
        print("Fiche chantier")
    elif choix == "2":
        print("Devis")
    elif choix == "0":
        print("Au revoir")
    else:
        print("Choix inconnu")
```

**Analogie BTP :** le menu est le tableau de bord du conducteur de travaux ; chaque commande ouvre une opération distincte. L'utilisateur doit toujours pouvoir quitter l'application.

**Mini-exercice :** ajouter l'option `3. Afficher le nombre de postes`.

## 2. Pourquoi sauvegarder ? Mémoire et fichiers

Les variables d'un programme sont généralement perdues à la fin de son exécution. Un fichier permet de conserver les informations entre deux lancements. Le format **JSON** représente des données structurées de manière lisible par de nombreux logiciels.

```json
{
  "reference": "CH-2026-001",
  "longueur": 6.0,
  "postes": [
    {"designation": "Parpaings", "quantite": 473, "prix_unitaire": 1.8}
  ]
}
```

Correspondances courantes : objet JSON ↔ dictionnaire Python ; tableau JSON ↔ liste Python ; chaîne ↔ `str` ; nombre ↔ `int` ou `float` ; booléen ↔ `bool` ; `null` ↔ `None`. JSON n'accepte pas les commentaires et utilise `true`, `false`, `null` (minuscules).

## 3. Écrire un fichier JSON

```python
import json

donnees = {
    "reference": "CH-2026-001",
    "budget_previsionnel": 3053.40
}

with open("chantier.json", "w", encoding="utf-8") as fichier:
    json.dump(donnees, fichier, ensure_ascii=False, indent=2)
```

`with open(...)` ferme automatiquement le fichier. Le mode `"w"` **remplace** le contenu existant. `encoding="utf-8"` conserve les accents ; `indent=2` rend le fichier lisible ; `ensure_ascii=False` évite d'échapper inutilement les caractères accentués.

**Attention :** le chemin relatif `chantier.json` dépend du **répertoire de travail courant** depuis lequel Python est lancé, pas nécessairement de l'emplacement du script.

## 4. Lire un fichier JSON

```python
with open("chantier.json", "r", encoding="utf-8") as fichier:
    donnees_chargees = json.load(fichier)
print(donnees_chargees["reference"])
```

`json.dump` écrit un objet dans un fichier ; `json.load` lit depuis un fichier. `json.dumps` et `json.loads` travaillent sur des **chaînes de caractères**, pas directement sur des fichiers.

**Mini-exercice :** sauvegarder puis recharger une liste de deux postes ; vérifier que les quantités sont identiques avant et après.

## 5. Erreurs et exceptions : ne pas planter sur une saisie

```python
try:
    quantite = float(input("Quantité : "))
except ValueError:
    print("Saisissez un nombre valide.")
```

Le bloc `try` contient une opération susceptible d'échouer. `except ValueError` intercepte uniquement l'erreur de conversion. On évite `except:` sans type, qui masquerait aussi des erreurs de programmation.

### Redemander jusqu'à une saisie valide

```python
def saisir_montant_positif(message):
    while True:
        try:
            valeur = float(input(message))
            if valeur >= 0:
                return valeur
            print("Le montant ne peut pas être négatif.")
        except ValueError:
            print("Veuillez saisir un nombre (exemple : 120.50).")
```

Ici, `while True` est volontaire : la fonction se termine avec `return` dès qu'une valeur valide est saisie. Pour des données financières professionnelles, on préférerait à terme `Decimal` ; dans ce TP, `float` et un affichage à deux décimales suffisent.

## 6. Erreurs possibles à l'ouverture d'un fichier

```python
import json

try:
    with open("chantier.json", "r", encoding="utf-8") as fichier:
        donnees = json.load(fichier)
except FileNotFoundError:
    print("Aucun fichier de chantier trouvé.")
except json.JSONDecodeError:
    print("Le fichier JSON est invalide.")
```

**Erreur fréquente :** croire qu'un fichier JSON correctement formé contient forcément les bonnes clés et des données cohérentes. Les contrôles de structure et les validations métier restent nécessaires.

## 7. Suivi budgétaire : prévu, réel, écart

Le coût prévisionnel est **3 053,40 € HT**. Les dépenses réelles du chantier pilote sont : parpaings 900 €, béton 540 €, main-d'œuvre 1 890 €, soit **3 330 € HT**.

```python
budget_prevu = 3053.40
depenses_reelles = 3330.00
ecart = depenses_reelles - budget_prevu
pourcentage = ecart / budget_prevu * 100 if budget_prevu > 0 else 0
print(f"Écart : {ecart:+.2f} € ({pourcentage:+.2f} %)")
```

Une valeur positive signifie un **dépassement**, une valeur négative une **économie**. Pour un budget prévisionnel nul, le pourcentage d'écart n'est pas défini : l'exemple affiche 0 uniquement pour éviter une division par zéro ; l'application finale devra indiquer explicitement « non calculable » dans ce cas.

**Mini-exercice :** déterminer l'écart du poste main-d'œuvre : 1 890 € − 1 680 € = **+210 €**.

## 8. Associer les dépenses aux postes

```python
postes = [
    {"designation": "Parpaings", "quantite": 473, "prix_unitaire": 1.80, "reel": 900.00},
    {"designation": "Béton", "quantite": 3.6, "prix_unitaire": 145.00, "reel": 540.00},
    {"designation": "Main-d'œuvre", "quantite": 40, "prix_unitaire": 42.00, "reel": 1890.00}
]

for poste in postes:
    prevu = poste["quantite"] * poste["prix_unitaire"]
    ecart = poste["reel"] - prevu
    print(poste["designation"], f"écart : {ecart:+.2f} €")
```

Les écarts sont respectivement +48,60 €, +18 € et +210 €, soit +276,60 € au total (environ +9,06 %).

## 9. Assembler l'application : fonctions et responsabilités

Prévoir des fonctions distinctes pour : afficher le chantier ; afficher le devis ; saisir les dépenses ; afficher le bilan ; sauvegarder ; charger ; afficher le menu. Le menu ne doit pas contenir tous les calculs : il **appelle** les fonctions adaptées.

**Conseil de conception :** les données sont regroupées dans un dictionnaire principal :

```python
dossier = {
    "chantier": {"reference": "CH-2026-001", "longueur": 6.0, "largeur": 4.0},
    "postes": []
}
```

Les clés choisies doivent être identiques lors de la sauvegarde et du chargement. Pour la mission, on ne demande ni interface graphique, ni base de données, ni gestion multiutilisateur.

## 10. Plan de recette

| Test | Action | Attendu |
|---|---|---|
| T1 | Afficher le devis initial | 3 053,40 € HT |
| T2 | Saisir 900, 540 et 1 890 € | Réel 3 330 € ; écart +276,60 € |
| T3 | Sauvegarder puis relancer et charger | Valeurs conservées |
| T4 | Charger un fichier absent | Message clair ; application toujours utilisable |
| T5 | Saisir un texte pour une dépense | Nouvelle saisie demandée |
| T6 | Saisir une option de menu inconnue | Message d'erreur, retour au menu |

## 11. Erreurs fréquentes

- `FileNotFoundError` : fichier absent ou répertoire de travail différent.
- `JSONDecodeError` : contenu JSON mal formé.
- `KeyError` : champ attendu absent du fichier.
- `ValueError` : saisie non convertible en nombre.
- Écrasement involontaire : ouverture en mode `"w"`.
- Écart inversé : calculer prévu − réel au lieu de réel − prévu.

## 12. Exercices de consolidation et mémo

1. Construire un menu `while` avec trois choix.
2. Sauvegarder un dictionnaire dans `test.json` et le recharger.
3. Intercepter une saisie alphabétique à la place d'un prix.
4. Calculer les écarts par poste et l'écart total.
5. Expliquer pourquoi la sauvegarde doit être testée après un redémarrage du programme.

| Élément | Utilité |
|---|---|
| `import json` | bibliothèque JSON |
| `json.dump(objet, fichier)` | sauvegarder |
| `json.load(fichier)` | recharger |
| `with open(..., "w")` | ouvrir en écriture |
| `with open(..., "r")` | ouvrir en lecture |
| `try` / `except ValueError` | gérer une conversion invalide |
| `except FileNotFoundError` | gérer un fichier absent |

**Bilan des quatre séances :** vous savez écrire une application Python en ligne de commande utilisant calculs, conditions, boucles, listes, dictionnaires, fonctions et fichiers JSON. Les chiffres restent des estimations pédagogiques et ne remplacent pas un devis BTP professionnel.
