# BatiCalc — Séance 2 : boucles, listes et devis

> **CESI — Prépa 1 | Cours étudiant | Mission 02 | 4 h cours et TP compris**  
> **Prérequis :** séance 1 (variables, `input`, calculs, conditions).  
> **Objectif métier :** transformer des quantités de chantier en devis multiposte.

## Compétences visées

À l'issue de la séance, vous pourrez expliquer et utiliser `for`, `while`, `range`, les listes, les indices, `append`, `len`, les accumulateurs et les parcours synchronisés de listes. Vous saurez distinguer une boucle bornée d'une boucle conditionnelle.

## 1. Pourquoi répéter des instructions ?

Un devis comprend plusieurs postes. Copier-coller trois fois un calcul semble simple, mais devient difficile à maintenir lorsque l'entreprise ajoute dix matériaux. **Analogie BTP :** on applique la même opération de contrôle à chaque ligne d'un bon de livraison, plutôt que d'écrire une procédure différente pour chaque ligne.

```python
prix = [1.80, 145.00, 42.00]
for montant in prix:
    print(f"Prix unitaire : {montant:.2f} €")
```

La variable `montant` prend successivement chaque valeur. **À retenir :** les instructions indentées appartiennent à la boucle.

## 2. La boucle `for` et `range()`

Une boucle `for` est adaptée lorsque l'on connaît une collection à parcourir ou un nombre d'itérations.

```python
for numero in range(1, 4):
    print("Poste", numero)
```

`range(1, 4)` produit 1, 2 et 3 ; la borne supérieure est exclue. `range(3)` produit 0, 1 et 2.

```python
for i in range(3):
    print("Indice :", i)
```

**Erreur fréquente :** croire que `range(1, 4)` produit quatre valeurs. **Mini-exercice :** afficher les numéros des cinq contrôles de chantier, de 1 à 5 inclus.

## 3. Les listes : regrouper des données

Une liste est une collection ordonnée, modifiable, dont les éléments sont accessibles par indice. Les indices commencent à **zéro**.

```python
materiaux = ["Parpaings", "Béton", "Main-d'œuvre"]
print(materiaux[0])       # Parpaings
print(materiaux[-1])      # Main-d'œuvre
print(len(materiaux))     # 3
```

On peut modifier ou ajouter un élément :

```python
materiaux[0] = "Parpaings creux"
materiaux.append("Transport")
print(materiaux)
```

`len` renvoie le nombre d'éléments. `append` ajoute **un élément** à la fin. Une liste vide se crée avec `[]`.

**Attention :** `materiaux[4]` provoque `IndexError` si la liste ne contient que quatre éléments (indices 0 à 3). Évitez de confondre **indice** et **position humaine**.

### Listes de nombres et agrégats

```python
quantites = [473, 3.6, 40]
print(sum(quantites))  # Calcul valide en Python, mais addition métier sans sens !
```

Le code fonctionne, mais additionner des pièces, des m³ et des heures est une erreur métier. Une somme n'est pertinente que pour des grandeurs homogènes, comme des montants en euros.

**Mini-exercice :** créer la liste `[120, 85, 40]` représentant trois coûts en euros, puis afficher leur somme et leur moyenne.

## 4. Parcourir une liste : valeurs ou indices ?

```python
noms = ["Parpaings", "Béton", "Main-d'œuvre"]
for nom in noms:
    print(nom)

for i in range(len(noms)):
    print(i, noms[i])
```

Le parcours par valeur est souvent plus lisible. Le parcours par indice est utile dans ce TP pour associer les éléments de **trois listes parallèles**.

```python
designations = ["Parpaings", "Béton", "Main-d'œuvre"]
quantites = [473, 3.6, 40]
prix_unitaires = [1.80, 145.00, 42.00]

for i in range(len(designations)):
    print(designations[i], quantites[i] * prix_unitaires[i])
```

Les trois listes doivent avoir exactement la même longueur et conserver le même ordre. Ce modèle est **transitoire** : la séance 3 introduira les dictionnaires pour mieux regrouper les données d'un poste.

## 5. Accumulateur : calculer un total

Un accumulateur conserve un résultat intermédiaire, mis à jour à chaque itération. **Analogie :** le total du devis augmente au fur et à mesure de l'ajout des postes.

```python
total_ht = 0.0
for i in range(len(designations)):
    montant_ligne = quantites[i] * prix_unitaires[i]
    total_ht += montant_ligne  # équivaut à total_ht = total_ht + montant_ligne
print(f"Total HT : {total_ht:.2f} €")
```

Pour le chantier de référence : parpaings 851,40 €, béton 522,00 €, main-d'œuvre 1 680,00 €, soit **3 053,40 € HT**.

**Erreur fréquente :** réinitialiser `total_ht = 0` **dans** la boucle, ce qui ne conserve que le dernier poste. **Mini-exercice :** calculer le montant du poste le plus coûteux, puis afficher son nom (sans utiliser `max` dans un premier temps).

## 6. La boucle `while` : répéter jusqu'à une condition

`while` est adaptée quand on ignore à l'avance combien de saisies l'utilisateur effectuera.

```python
reponse = ""
while reponse != "n":
    reponse = input("Ajouter un autre poste ? (o/n) : ").strip().lower()
    if reponse != "o" and reponse != "n":
        print("Répondez par o ou n.")
```

**Attention aux boucles infinies :** une variable utilisée dans la condition doit pouvoir changer. La méthode `strip()` supprime les espaces en début et fin de texte ; `lower()` convertit en minuscules.

### Validation d'une quantité (saisie numérique supposée)

```python
quantite = float(input("Quantité : "))
while quantite <= 0:
    print("La quantité doit être positive.")
    quantite = float(input("Quantité : "))
```

Ce code ne gère pas une saisie alphabétique : les exceptions seront introduites en séance 4.

## 7. Le `break` et le `continue` (complément)

`break` interrompt immédiatement la boucle ; `continue` passe à l'itération suivante. Ils sont utiles, mais ne doivent pas masquer une logique simple qui peut être exprimée dans la condition de boucle.

```python
for montant in [851.4, 522.0, 1680.0]:
    if montant < 600:
        continue
    print("Poste important :", montant)
```

## 8. Construire le devis BatiCalc

Reprendre les **résultats validés** de la séance 1 : 473 parpaings et 3,60 m³ de béton ; ajouter 40 h de main-d'œuvre. Dans la première version, ces quantités peuvent être fixées pour isoler l'apprentissage des listes. Ensuite, réutiliser les calculs de S1.

```python
designations = ["Parpaings", "Béton", "Main-d'œuvre"]
quantites = [473, 3.60, 40]
prix_unitaires = [1.80, 145.00, 42.00]

total = 0.0
for i in range(len(designations)):
    montant = quantites[i] * prix_unitaires[i]
    total += montant
    print(f"{designations[i]:15} {montant:8.2f} €")
print(f"TOTAL HT : {total:.2f} €")
```

## 9. Tester et déboguer

| Cas | Attendu |
|---|---|
| Chantier de référence | 3 053,40 € HT |
| Prix des parpaings doublé | 3 904,80 € HT |
| Ajout d'un poste « Transport », 1 × 120 € | 3 173,40 € HT |
| Trois listes de longueurs différentes | Situation à détecter, sinon risque d'`IndexError` |
| Liste de postes vide | Total 0 €, sans plantage |

En cas d'erreur, lire la dernière ligne du traceback, puis inspecter la valeur de l'indice et la longueur de chaque liste. Le résultat métier doit être vérifié **indépendamment** du programme.

## 10. Exercices de consolidation

1. Afficher les postes du devis numérotés de 1 à 3.
2. Ajouter un quatrième poste « Transport », 1 unité à 120 €.
3. Compter le nombre de postes dont le montant dépasse 500 €.
4. Demander à l'utilisateur s'il souhaite ajouter un poste ; recommencer jusqu'à `n`.
5. Afficher le pourcentage du coût total représenté par la main-d'œuvre (environ 55,02 % pour le devis de référence).

## 11. Fiche mémo

| Élément | Usage |
|---|---|
| `[]` | créer une liste |
| `liste[0]` | accéder au premier élément |
| `len(liste)` | compter les éléments |
| `liste.append(x)` | ajouter un élément |
| `for x in liste:` | parcourir les valeurs |
| `for i in range(n):` | parcourir des indices |
| `while condition:` | répéter sous condition |
| `total += montant` | cumuler des valeurs |
| `break` / `continue` | interrompre / sauter une itération |

**Préparation au TP2 :** être capable d'expliquer pourquoi trois listes parallèles exigent une synchronisation stricte. C'est le problème résolu en séance 3.
