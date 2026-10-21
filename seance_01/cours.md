# BatiCalc — Séance 1 : les fondamentaux de Python

> **CESI — Prépa 1 | Projet BatiCalc | Cours étudiant | Mission 01**  
> **Durée de la séance complète : 4 h**, cours, démonstrations et TP compris.  
> **Prérequis :** savoir décrire un algorithme simple (séquence, variable, test).  
> **Environnement :** Python 3, VS Code et extension Python. Aucune bibliothèque externe.

## Objectifs d'apprentissage

À l'issue de cette séance, vous saurez :

1. créer et exécuter un script Python ;
2. utiliser les variables et reconnaître les types `int`, `float`, `str` et `bool` ;
3. afficher un résultat, lire une saisie et convertir du texte en nombre ;
4. traduire une formule géométrique en expression Python ;
5. utiliser les comparaisons et les conditions `if`, `elif`, `else` ;
6. arrondir correctement une quantité de matériaux ;
7. vérifier votre programme avec des jeux d'essai.

**Fil rouge :** BÂTI33 Construction veut automatiser le calcul des matériaux d'un garage. Les dimensions de référence sont : longueur 6 m, largeur 4 m, hauteur des murs 2,5 m, porte de 2,4 × 2,1 m, dalle de 0,15 m d'épaisseur. Les résultats sont des estimations pédagogiques et non des métrés professionnels.

---

## 1. Pourquoi Python ? De l'algorithme au programme

Un **algorithme** est une suite finie d'instructions pour résoudre un problème. Un **programme** est sa traduction dans un langage que l'ordinateur peut exécuter. Python est un langage généraliste, lisible et utilisé notamment en automatisation, traitement de données, calcul scientifique et développement d'applications.

**Analogie BTP :** le plan décrit l'ouvrage à réaliser ; le programme décrit précisément les opérations que la machine doit effectuer. Une consigne imprécise produit un résultat imprévisible, même si la machine l'exécute rapidement.

### 1.1 Premier programme

Créez un fichier `bonjour.py` :

```python
print("Bonjour BÂTI33 Construction !")
print("Bienvenue dans le projet BatiCalc")
```

`print()` affiche une information dans le terminal. Le texte est délimité par des guillemets ; chaque instruction se termine normalement par un retour à la ligne, sans point-virgule obligatoire.

Dans un terminal ouvert dans le dossier du fichier :

```bash
python --version
python bonjour.py
```

Sur certaines installations Windows, utilisez `py --version` puis `py bonjour.py`. Dans VS Code, sélectionnez l'interpréteur Python via **Python: Select Interpreter** si nécessaire.

### 1.2 Script, interpréteur, terminal

- Le **script** est le fichier texte `.py` contenant vos instructions.
- L'**interpréteur Python** exécute ces instructions.
- Le **terminal** permet de lancer le script et de voir ses messages.
- VS Code est un **éditeur de code**, pas le langage Python lui-même.

Python exécute habituellement les instructions d'un script de haut en bas. L'ordre est donc important.

```python
print("Début")
print("Calcul en cours")
print("Fin")
```

### 1.3 Commentaires et lisibilité

Un commentaire commence par `#`. Il est ignoré lors de l'exécution.

```python
# Dimensions du garage, exprimées en mètres
longueur = 6
largeur = 4
print(longueur * largeur)  # Surface au sol en m²
```

Privilégiez des noms explicites : `surface_murs` est plus compréhensible que `sm`.

**À essayer (5 min) :** créez `bonjour.py`, ajoutez votre prénom et la référence `CH-2026-001`, puis exécutez le fichier deux fois après modification.

---

## 2. Les variables : mémoriser des informations

Une **variable** associe un nom à une valeur. On peut la voir comme une case étiquetée dans laquelle le programme retrouve une information. En Python, `=` est une **affectation** : il ne signifie pas « est égal à » au sens d'un test.

```python
longueur = 6
largeur = 4
surface_sol = longueur * largeur
print(surface_sol)  # 24
```

La valeur d'une variable peut changer :

```python
longueur = 6
longueur = 7
print(longueur)  # 7
```

Python distingue les majuscules et minuscules : `longueur` et `Longueur` sont deux noms différents.

### 2.1 Règles de nommage

Un identifiant peut contenir des lettres, des chiffres et `_`, mais ne doit pas commencer par un chiffre ni être un mot réservé (`if`, `else`, etc.). La convention courante est `snake_case` : `surface_nette_murs`.

```python
hauteur_mur = 2.5     # Correct
# 2hauteur = 2.5      # Incorrect : commence par un chiffre
# if = 2.5           # Incorrect : mot réservé
```

### 2.2 Quatre types fondamentaux

| Type | Signification | Exemple BTP |
|---|---|---|
| `int` | Nombre entier | `nombre_portes = 1` |
| `float` | Nombre à virgule flottante | `hauteur = 2.5` |
| `str` | Chaîne de caractères | `reference = "CH-2026-001"` |
| `bool` | Valeur logique | `chantier_valide = True` |

```python
reference = "CH-2026-001"
longueur = 6
hauteur = 2.5
chantier_valide = True

print(type(reference))       # <class 'str'>
print(type(longueur))        # <class 'int'>
print(type(hauteur))         # <class 'float'>
print(type(chantier_valide)) # <class 'bool'>
```

**Important :** les nombres décimaux s'écrivent avec un **point** en Python (`2.5`), et non avec une virgule (`2,5`). Les `float` sont des approximations binaires : certains calculs décimaux ne sont pas représentés exactement. Pour le TP1, l'affichage à deux décimales suffit ; les calculs monétaires rigoureux seront abordés ultérieurement.

### 2.3 Erreurs typiques

```python
longueur = 6
# print(longeur)  # NameError : faute dans le nom
```

**Exercice 1 (5 min).** Déclarez `nom_chantier`, `longueur`, `largeur`, `hauteur`, `porte_presente`. Affichez leurs valeurs et leurs types. Modifiez la largeur et observez le résultat.

---

## 3. Entrées et sorties : dialoguer avec l'utilisateur

### 3.1 Afficher avec `print()`

```python
longueur = 6
print("Longueur :", longueur, "m")
```

Pour composer un message lisible, utilisez une **f-string** :

```python
surface = 24.0
print(f"Surface au sol : {surface:.2f} m²")
```

`:.2f` demande un affichage avec deux chiffres après le point décimal. Cela **ne modifie pas** la valeur stockée dans `surface`.

### 3.2 Lire avec `input()`

```python
nom = input("Nom du client : ")
print(f"Client : {nom}")
```

**Point essentiel :** `input()` renvoie toujours une chaîne de caractères, même si l'utilisateur tape `6`.

```python
longueur_texte = input("Longueur (m) : ")
print(type(longueur_texte))  # <class 'str'>
```

Pour calculer, il faut convertir :

```python
longueur = float(input("Longueur (m) : "))
largeur = float(input("Largeur (m) : "))
surface = longueur * largeur
print(f"Surface : {surface:.2f} m²")
```

`int()` convertit une valeur compatible en entier ; `float()` convertit une chaîne représentant un nombre décimal. Attention : `int("2.5")` échoue ; `int(2.5)` donne `2` en supprimant la partie décimale, **sans arrondir**.

### 3.3 Comprendre les erreurs de conversion

```python
# float("abc")  # ValueError : texte non convertible
# float("2,5")  # ValueError : virgule non acceptée directement
```

Dans le TP1, on demandera de saisir les décimales avec un point. La gestion des saisies non numériques par `try/except` n'est pas exigée à cette séance.

**Exercice 2 (10 min).** Demandez la longueur et la largeur d'une dalle ; affichez les deux valeurs avec deux décimales et calculez la surface. Essayez une saisie `4`, puis `4.5`, puis `quatre` : que se passe-t-il ?

---

## 4. Opérateurs arithmétiques et priorité des calculs

| Opérateur | Sens | Exemple | Résultat |
|---|---|---|---|
| `+` | Addition | `6 + 4` | `10` |
| `-` | Soustraction | `6 - 4` | `2` |
| `*` | Multiplication | `6 * 4` | `24` |
| `/` | Division réelle | `7 / 2` | `3.5` |
| `//` | Division entière par plancher | `7 // 2` | `3` |
| `%` | Reste de division | `7 % 2` | `1` |
| `**` | Puissance | `3 ** 2` | `9` |

Les parenthèses rendent la formule explicite et évitent les erreurs de priorité :

```python
longueur = 6
largeur = 4
perimetre = 2 * (longueur + largeur)  # 20 m
```

Sans parenthèses, `2 * longueur + largeur` donnerait `16`, un résultat incorrect.

### 4.1 Respecter les unités

- Longueur, largeur, hauteur, épaisseur : **m**.
- Périmètre : **m**.
- Surface : **m²**.
- Volume : **m³**.
- Quantité de parpaings : **pièces**.

**Analogie :** additionner une surface et un volume revient à additionner des mètres carrés et des mètres cubes ; le programme peut le faire numériquement, mais le résultat n'a aucun sens physique. C'est au développeur de contrôler la formule.

### 4.2 Formules du chantier pilote

Pour un garage rectangulaire de longueur `L`, largeur `l`, hauteur des murs `h` et épaisseur de dalle `e` :

$$
P = 2(L+l),\quad S_{\text{sol}}=L\times l,\quad S_{\text{murs bruts}}=P\times h
$$

$$
S_{\text{porte}}=L_{\text{porte}}\times h_{\text{porte}},\quad S_{\text{murs nets}}=S_{\text{murs bruts}}-S_{\text{porte}}
$$

$$
V_{\text{dalle}}=S_{\text{sol}}\times e
$$

En Python :

```python
longueur = 6.0
largeur = 4.0
hauteur = 2.5
epaisseur_dalle = 0.15
largeur_porte = 2.4
hauteur_porte = 2.1

perimetre = 2 * (longueur + largeur)
surface_sol = longueur * largeur
surface_brute = perimetre * hauteur
surface_porte = largeur_porte * hauteur_porte
surface_nette = surface_brute - surface_porte
volume_beton = surface_sol * epaisseur_dalle

print(f"Périmètre : {perimetre:.2f} m")
print(f"Surface brute : {surface_brute:.2f} m²")
print(f"Surface nette : {surface_nette:.2f} m²")
print(f"Volume de béton : {volume_beton:.2f} m³")
```

**Résultats attendus :** périmètre 20 m ; surface au sol 24 m² ; murs bruts 50 m² ; porte 5,04 m² ; murs nets 44,96 m² ; béton 3,60 m³.

**Exercice 3 (10 min).** Pour une dalle de 5 m × 3 m et d'épaisseur 0,12 m, calculez sa surface et son volume. Résultats : 15 m² et 1,80 m³.

---

## 5. Arrondir une quantité de matériaux

Un parpaing standard du dossier pédagogique couvre nominalement `0.20 × 0.50 = 0.10 m²` de mur. On majore la quantité théorique de 5 % pour les pertes et découpes.

$$
N = \left\lceil \frac{S_{\text{murs nets}}}{0{,}10}\times 1{,}05\right\rceil
$$

Le symbole `⌈ ⌉` signifie **arrondir à l'entier supérieur**. On ne peut pas commander une fraction de parpaing.

```python
import math

surface_nette = 44.96
surface_parpaing = 0.10
marge_pertes = 0.05

quantite_theorique = surface_nette / surface_parpaing
quantite_avec_marge = quantite_theorique * (1 + marge_pertes)
nombre_parpaings = math.ceil(quantite_avec_marge)

print(nombre_parpaings)  # 473
```

`math` est un **module de la bibliothèque standard** de Python. `import math` donne accès notamment à `math.ceil()` : aucune installation supplémentaire n'est nécessaire.

**Attention :** `round()` arrondit au plus proche, ce qui ne convient pas pour une commande où il faut couvrir la totalité du besoin. `int()` tronque vers zéro et ne convient pas non plus.

**Exercice 4 (5 min).** Une surface nette vaut 18,2 m². Combien de parpaings faut-il commander avec une marge de 5 % ? Réponse : `math.ceil(18.2 / 0.10 * 1.05) = 192`.

---

## 6. Booléens, comparaisons et décisions

Dans un chantier, certaines données doivent être vérifiées **avant** de lancer les calculs : une longueur ne peut pas être négative et une ouverture ne peut pas être plus grande que la surface des murs.

### 6.1 Comparer des valeurs

| Opérateur | Signification | Exemple |
|---|---|---|
| `==` | Égal à | `longueur == 6` |
| `!=` | Différent de | `longueur != 6` |
| `<` | Inférieur à | `longueur < 0` |
| `<=` | Inférieur ou égal | `longueur <= 0` |
| `>` | Supérieur à | `longueur > 0` |
| `>=` | Supérieur ou égal | `longueur >= 6` |

Une comparaison produit `True` ou `False` :

```python
longueur = 6
print(longueur > 0)  # True
print(longueur == 4) # False
```

Ne confondez pas `=` (affectation) et `==` (comparaison).

### 6.2 `if`, `else` et indentation

```python
longueur = float(input("Longueur (m) : "))

if longueur <= 0:
    print("Erreur : la longueur doit être positive.")
else:
    print("Longueur acceptée.")
```

La condition se termine par `:`. Les instructions qui en dépendent sont **indentées** (convention : quatre espaces). Python utilise cette indentation pour délimiter les blocs ; elle n'est pas simplement décorative.

### 6.3 Plusieurs possibilités avec `elif`

```python
surface_sol = 24

if surface_sol < 20:
    print("Petit chantier")
elif surface_sol <= 40:
    print("Chantier moyen")
else:
    print("Grand chantier")
```

Ces seuils sont fictifs et ne correspondent pas à une classification réglementaire.

### 6.4 Combiner les conditions : `and`, `or`, `not`

```python
longueur = 6
largeur = 4
hauteur = 2.5

dimensions_valides = longueur > 0 and largeur > 0 and hauteur > 0
print(dimensions_valides)  # True
```

- `and` : toutes les conditions doivent être vraies.
- `or` : au moins une condition doit être vraie.
- `not` : inverse un booléen.

**Exercice 5 (10 min).** Écrivez une condition qui affiche une erreur si au moins une des trois dimensions est nulle ou négative. Puis écrivez une condition qui refuse une porte dont la surface est supérieure ou égale à la surface brute des murs.

---

## 7. Construire un programme sûr par étapes

Une démarche simple pour le TP1 :

1. **Entrées** : demander les dimensions du garage.
2. **Validation** : refuser les dimensions nulles ou négatives.
3. **Calculs intermédiaires** : périmètre, surfaces, volume.
4. **Validation métier** : vérifier que la porte est plus petite que les murs.
5. **Calcul final** : nombre de parpaings avec marge.
6. **Sorties** : afficher des résultats avec leurs unités.

### 7.1 Pourquoi valider avant de calculer ?

Sans contrôle, une largeur négative peut conduire à une surface absurde. Le programme doit éviter de présenter ce résultat comme une estimation valable.

Voici un exemple complet de **validation des dimensions** (le reste des calculs constitue le TP) :

```python
longueur = float(input("Longueur (m) : "))
largeur = float(input("Largeur (m) : "))
hauteur = float(input("Hauteur (m) : "))

if longueur <= 0 or largeur <= 0 or hauteur <= 0:
    print("Erreur : toutes les dimensions doivent être positives.")
else:
    perimetre = 2 * (longueur + largeur)
    surface_brute = perimetre * hauteur
    surface_porte = 2.4 * 2.1

    if surface_porte >= surface_brute:
        print("Erreur : la porte est trop grande pour les murs.")
    else:
        print("Dimensions cohérentes : calcul possible.")
```

**Limite volontaire :** le programme ne vérifie pas encore que la porte peut géométriquement tenir sur un mur précis ; il vérifie seulement la cohérence de surface demandée par le TP1.

### 7.2 Lire les messages d'erreur

| Message | Cause fréquente | Réaction |
|---|---|---|
| `SyntaxError` | Parenthèse ou `:` manquant | Vérifier la ligne signalée et la précédente |
| `IndentationError` | Bloc mal indenté | Vérifier les quatre espaces sous `if` ou `else` |
| `NameError` | Nom de variable incorrect | Vérifier l'orthographe et l'affectation préalable |
| `TypeError` | Opération incompatible avec le type | Examiner `type(...)` et les conversions |
| `ValueError` | Conversion impossible, ex. `float("abc")` | Vérifier la saisie utilisateur |
| `ZeroDivisionError` | Division par zéro | Contrôler le dénominateur |

Pour diagnostiquer, affichez les valeurs intermédiaires :

```python
print("DEBUG surface brute =", surface_brute)
```

Retirez ces messages de débogage de la version finale si vous n'en avez plus besoin.

---

## 8. Tester : vérifier le programme plutôt que supposer qu'il marche

Un programme qui fonctionne une fois n'est pas nécessairement correct. On teste des cas **nominaux**, des **limites** et des **entrées invalides**.

| Test | Entrées | Résultat attendu |
|---|---|---|
| T1 | L=6, l=4, h=2,5 | 44,96 m² nets ; 3,60 m³ ; 473 parpaings |
| T2 | L=0, l=4, h=2,5 | Message d'erreur, pas d'estimation |
| T3 | L=6, l=-4, h=2,5 | Message d'erreur, pas d'estimation |
| T4 | L=6, l=4, h=0 | Message d'erreur, pas d'estimation |
| T5 | L=1, l=1, h=1 | Porte trop grande, pas d'estimation |

Pour T1, détaillons le raisonnement :

```text
Périmètre                  = 2 × (6 + 4)       = 20 m
Surface brute des murs     = 20 × 2,5          = 50 m²
Surface de la porte        = 2,4 × 2,1         = 5,04 m²
Surface nette des murs     = 50 − 5,04         = 44,96 m²
Volume de béton           = 6 × 4 × 0,15      = 3,60 m³
Parpaings avec 5 % pertes = ceil(44,96 / 0,10 × 1,05) = 473
```

Un test est **réussi** si le résultat observé correspond au résultat attendu. Notez les anomalies, corrigez, puis rejouez les tests.

---

## 9. Mini-défis de consolidation

Ces exercices peuvent être réalisés pendant les démonstrations ou en autonomie avant le TP.

**Défi A — Surface d'une pièce (5 min).** Demander deux dimensions et afficher la surface avec deux décimales. Refuser les dimensions non positives.

**Défi B — Volume d'une dalle (5 min).** Demander longueur, largeur et épaisseur. Afficher le volume en m³. Tester 5 × 3 × 0,12.

**Défi C — Nombre de sacs (5 min).** Une consommation fictive de mortier est de 1,7 sac par m². Pour une surface de 12,5 m², calculer le nombre entier de sacs à commander avec `math.ceil()`.

**Défi D — Catégorisation (5 min).** À partir de la surface au sol, afficher « petit », « moyen » ou « grand » chantier en utilisant les seuils fictifs de la section 6.3.

---

## 10. Fiche mémo Python — Séance 1

```python
# Commentaire
nom = "Garage"             # str
nombre = 4                 # int
hauteur = 2.5              # float
valide = True              # bool

print(nom)                 # Affichage
saisie = input("Valeur : ") # Renvoie str
valeur = float(saisie)     # Conversion en float

surface = 6 * 4            # Multiplication
carre = 3 ** 2            # Puissance

if valeur > 0:
    print(f"Valeur : {valeur:.2f}")
elif valeur == 0:
    print("Valeur nulle")
else:
    print("Valeur négative")

import math
pieces = math.ceil(12.4)  # 13
```

### Questions d'autoévaluation

1. Quelle différence existe entre `=` et `==` ?
2. Quel type de valeur renvoie `input()` ?
3. Pourquoi utiliser `float()` après `input()` pour une longueur ?
4. Quelle différence existe entre `int(2.9)`, `round(2.9)` et `math.ceil(2.9)` ?
5. Pourquoi la formule du périmètre contient-elle des parenthèses ?
6. Pourquoi faut-il vérifier les dimensions avant d'afficher une estimation ?
7. Quelle unité doit accompagner un volume de béton ?
8. Que signifie une erreur `IndentationError` ?

### Pour aller plus loin (hors objectifs obligatoires)

Lors des prochaines séances, nous découvrirons les **boucles** et les **listes** pour traiter plusieurs postes de devis, puis les **dictionnaires** et les **fonctions** pour structurer BatiCalc. Les **fichiers JSON** permettront enfin de conserver les données du chantier.

---

## 11. Passage au TP1

Ouvrez le fichier [`tp.md`](tp.md), puis créez ou complétez `exercices/bati_calc_s1.py`. Travaillez par incréments : saisies → contrôles → surfaces → volume → parpaings → tests. Conservez une version qui fonctionne à chaque étape.

**Critères de réussite :** calculs justes, unités affichées, saisies numériques converties, dimensions invalides refusées, résultats de référence reproduits et code lisible.

**Rappel métier :** BatiCalc est un outil pédagogique simplifié ; il ne remplace ni une étude de structure, ni un métré détaillé, ni un devis professionnel.
