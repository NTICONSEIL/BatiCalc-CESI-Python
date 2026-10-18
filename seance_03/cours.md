# BatiCalc — Séance 3 : dictionnaires, fonctions et code réutilisable

> **CESI — Prépa 1 | Cours étudiant | Mission 03 | 4 h cours et TP compris**  
> **Prérequis :** listes, boucles, conditions, calculs du devis.  
> **Objectif métier :** organiser les données de chantier et fiabiliser les calculs.

## Compétences visées

Créer et modifier un dictionnaire, parcourir ses clés et valeurs, construire une liste de dictionnaires, définir et appeler une fonction, distinguer paramètres, arguments et valeur de retour, et tester une fonction isolément.

## 1. Pourquoi les listes parallèles posent problème

Dans la séance 2, trois listes décrivent le même poste par un indice commun. Si l'on supprime un élément d'une seule liste, les prix et les quantités ne correspondent plus. **Analogie BTP :** conserver la désignation, la quantité et le prix sur une même fiche évite de mélanger les lignes de plusieurs devis.

## 2. Les dictionnaires : associer des clés à des valeurs

```python
poste = {
    "designation": "Parpaings",
    "quantite": 473,
    "prix_unitaire": 1.80,
    "unite": "pièce"
}
print(poste["designation"])
print(poste["quantite"] * poste["prix_unitaire"])
```

Un dictionnaire est une collection de couples **clé → valeur**. Ici, les clés sont des chaînes. Contrairement à une liste, on accède aux données par leur signification, non par leur position.

```python
poste["quantite"] = 480
poste["reference"] = "MAT001"
print(poste.get("fournisseur", "Non renseigné"))
```

`poste["fournisseur"]` provoquerait une `KeyError` si la clé n'existe pas. `get` permet une valeur par défaut. Ne pas confondre `poste["quantite"]` (accès) et `poste["quantite"] = 480` (modification).

### Parcourir un dictionnaire

```python
for cle, valeur in poste.items():
    print(cle, ":", valeur)
```

`keys()` donne les clés, `values()` les valeurs et `items()` les paires clé/valeur.

**Mini-exercice :** créer un dictionnaire `chantier` avec `reference`, `longueur`, `largeur`, `hauteur`. Afficher la surface au sol.

## 3. Les listes de dictionnaires : un devis complet

```python
postes = [
    {"designation": "Parpaings", "quantite": 473, "prix_unitaire": 1.80},
    {"designation": "Béton", "quantite": 3.6, "prix_unitaire": 145.00},
    {"designation": "Main-d'œuvre", "quantite": 40, "prix_unitaire": 42.00}
]
for poste in postes:
    montant = poste["quantite"] * poste["prix_unitaire"]
    print(poste["designation"], montant)
```

Cette structure regroupe les informations liées et facilite l'ajout d'un poste :

```python
postes.append({"designation": "Transport", "quantite": 1, "prix_unitaire": 120.00})
```

**Mini-exercice :** compter les postes dont le montant dépasse 500 €.

## 4. Fonctions : découper un problème

Une fonction est un bloc nommé qui réalise une tâche. **Analogie BTP :** un mode opératoire précis peut être réutilisé sur plusieurs chantiers, avec des dimensions différentes.

```python
def calculer_surface_sol(longueur, largeur):
    return longueur * largeur

surface = calculer_surface_sol(6, 4)
print(surface)  # 24
```

- `def` introduit la définition.
- `longueur` et `largeur` sont des **paramètres**.
- `6` et `4` sont les **arguments** passés à l'appel.
- `return` renvoie une valeur à l'appelant et termine l'exécution de la fonction.

Une fonction ne s'exécute pas simplement parce qu'elle est définie : il faut l'appeler.

## 5. `return` n'est pas `print`

```python
def afficher_total(total):
    print(f"Total : {total:.2f} €")

def calculer_total_ligne(quantite, prix):
    return quantite * prix

montant = calculer_total_ligne(473, 1.80)
afficher_total(montant)
```

`print` affiche une information, mais ne fournit pas le montant à d'autres calculs. Une fonction sans `return` explicite renvoie `None`. **Bonne pratique :** séparer les calculs des interactions avec l'utilisateur.

## 6. Portée des variables

```python
def calculer_volume(longueur, largeur, epaisseur):
    volume = longueur * largeur * epaisseur
    return volume

print(calculer_volume(6, 4, 0.15))
# print(volume)  # NameError : volume est local à la fonction
```

Une variable créée dans une fonction est généralement **locale**. Préférer le passage de paramètres aux variables globales implicites.

## 7. Composer plusieurs fonctions

```python
import math

def calculer_surface_murs(longueur, largeur, hauteur, porte_largeur, porte_hauteur):
    return 2 * (longueur + largeur) * hauteur - porte_largeur * porte_hauteur

def calculer_parpaings(surface_nette, surface_unitaire=0.10, taux_pertes=0.05):
    return math.ceil(surface_nette / surface_unitaire * (1 + taux_pertes))

def calculer_montant(poste):
    return poste["quantite"] * poste["prix_unitaire"]

def calculer_total(postes):
    total = 0.0
    for poste in postes:
        total += calculer_montant(poste)
    return total
```

Les **valeurs par défaut** (`surface_unitaire=0.10`) sont utilisées lorsqu'aucun argument n'est fourni. Les paramètres obligatoires précèdent les paramètres avec valeurs par défaut.

## 8. Refactorisation : changer la structure, pas les résultats

La refactorisation consiste à améliorer l'organisation interne du programme sans changer le comportement attendu. Notre référence reste **473 parpaings**, **3,60 m³** de béton et **3 053,40 € HT**. Toute modification doit conserver ces résultats.

### Exemple d'architecture simple

```python
def afficher_devis(postes):
    for poste in postes:
        print(poste["designation"], f'{calculer_montant(poste):.2f} €')
    print(f"TOTAL : {calculer_total(postes):.2f} €")
```

La fonction `afficher_devis` **dépend** des fonctions définies précédemment. Les définitions doivent être exécutées avant l'appel effectif.

## 9. Tester des fonctions indépendamment

```python
assert calculer_surface_murs(6, 4, 2.5, 2.4, 2.1) == 44.96 or abs(
    calculer_surface_murs(6, 4, 2.5, 2.4, 2.1) - 44.96
) < 1e-9
assert calculer_parpaings(44.96) == 473
assert abs(calculer_total(postes[:3]) - 3053.40) < 1e-9
```

Un `assert` vérifie une condition ; si elle est fausse, Python lève `AssertionError`. Les nombres flottants peuvent comporter de très petites erreurs de représentation : on préfère comparer leur **écart à une tolérance** plutôt que demander une égalité exacte. Pour les quantités de parpaings (entiers), l'égalité exacte convient.

## 10. Erreurs fréquentes et dépannage

| Erreur | Cause probable | Remède |
|---|---|---|
| `KeyError: 'quantite'` | Clé absente ou mal orthographiée | Vérifier `poste.keys()` |
| `TypeError` lors d'une multiplication | Prix stocké en chaîne | Convertir en `float` |
| Fonction renvoie `None` | `return` oublié | Ajouter `return resultat` |
| Résultat inchangé après modification | Fonction jamais appelée | Vérifier les appels |
| Mauvais total | Réinitialisation de l'accumulateur dans la boucle | Initialiser avant le parcours |

## 11. Exercices de consolidation

1. Créer un dictionnaire pour le béton et calculer son montant.
2. Convertir les trois listes de S2 en une liste de dictionnaires.
3. Écrire `calculer_montant(poste)` puis `calculer_total(postes)`.
4. Écrire `rechercher_poste(postes, designation)` qui renvoie le poste trouvé ou `None`.
5. Modifier la quantité de parpaings et vérifier que le total se met à jour.

## 12. Fiche mémo

| Syntaxe | Sens |
|---|---|
| `{ "cle": valeur }` | dictionnaire |
| `d["cle"]` | lecture d'une valeur |
| `d.get("cle", defaut)` | lecture avec valeur de secours |
| `d.items()` | couples clé-valeur |
| `[{}, {}]` | liste de dictionnaires |
| `def nom(parametre):` | définition de fonction |
| `return valeur` | résultat de fonction |
| `assert condition` | contrôle de test |

**Préparation à la séance 4 :** notre programme sait calculer un devis mais oublie tout quand il se termine. Nous apprendrons à sauvegarder les données et à suivre les dépenses réelles.
