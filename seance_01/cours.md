# BatiCalc — Séance 1 — Cours Python (enseignant)

**Public :** CESI prépa 1 ; bases d'algorithmique. **Durée :** 4 h avec TP. **Pré-requis :** algorithmes séquentiels et tests simples. **Outils :** Python 3, VS Code, extension Python.

## Compétences
1. Exécuter un script `.py` depuis le terminal.
2. Utiliser variables, types `str`, `int`, `float`, `bool`, affichage et saisie.
3. Calculer surfaces, volumes et quantités.
4. Vérifier la cohérence des données avec `if`, `elif`, `else`.
5. Tester un programme sur des cas nominaux et invalides.

## 0h00–0h30 — De l'algorithme au script Python
- Démontrer `python --version` (ou `py --version` sous Windows) puis `python bonjour.py`.
- Écrire :
```python
print("Bonjour BÂTI33")
```
- Insister sur l'exécution de haut en bas, les commentaires `#`, l'indentation et les erreurs de syntaxe.
- Analogie : un algorithme est une recette, Python en est une écriture exécutable.

## 0h30–1h15 — Variables, types, saisie et affichage
```python
nom_chantier = "Garage Dupont"   # str
longueur = 6                    # int
hauteur = 2.5                  # float
valide = True                  # bool
print(type(hauteur))
print(f"Chantier : {nom_chantier} — hauteur : {hauteur:.2f} m")
longueur = float(input("Longueur (m) : "))
```
**Explication essentielle :** `input()` renvoie toujours une chaîne ; `float()` convertit une valeur saisie. La virgule décimale française `2,5` ne fonctionne pas directement avec `float()` : saisir `2.5`.

**Micro-exercices :** déclarer largeur=4 ; calculer `surface = longueur * largeur` ; afficher à deux décimales ; tester `float("abc")` et expliquer l'erreur.

## 1h15–2h00 — Opérateurs et formules du BTP
- `+`, `-`, `*`, `/`, `**`, parenthèses ; distinguer `/` et `//`.
- Aire de dalle : `longueur * largeur` ; volume de dalle : `aire * epaisseur`.
- Périmètre : `2 * (longueur + largeur)` ; murs bruts : `perimetre * hauteur`.
- Surface nette : murs bruts moins ouverture ; unités m, m², m³.
- Quantité de parpaings : surface nette / 0,10 puis majoration de 5 % ; arrondir au supérieur avec `math.ceil`.
```python
import math
nombre = math.ceil((44.96 / 0.10) * 1.05)
print(nombre)  # 473
```
**Point pédagogique :** ne pas utiliser `round()` pour un besoin d'arrondi supérieur ; le nombre de pièces doit être entier.

## 2h00–2h45 — Conditions et contrôles
```python
longueur = float(input("Longueur (m) : "))
if longueur <= 0:
    print("Erreur : la longueur doit être positive.")
else:
    print("Longueur acceptée.")
```
- Comparaisons `==`, `!=`, `<`, `<=`, `>`, `>=` ; opérateurs `and`, `or`.
- Conditions en cascade et indentation ; `elif` pour distinguer trois situations.
- Contrôler : dimensions > 0 ; porte <= surface brute ; afficher message et ne pas poursuivre les calculs invalides.
- Limite du cours : ne pas exiger `try/except` avant la séance 4 ; annoncer que les caractères non numériques provoquent une erreur.

## 2h45–3h40 — Mission intégratrice
Distribuer le TP étudiant ; laisser les étudiants coder par incréments (saisie, surface, béton, parpaings, contrôle). Proposer un jeu de test à chaque incrément. Faire verbaliser les unités et l'arrondi.

## 3h40–4h00 — Recette et synthèse
Vérifier cas nominal 6 × 4 × 2,5 : murs nets 44,96 m², dalle 3,60 m³, 473 parpaings. Tester dimensions négatives et ouverture trop grande. Demander une explication orale de la différence entre `input`, `float` et `math.ceil`.

## Erreurs fréquentes et remédiations
- `TypeError` lors de calcul avec une chaîne : convertir la saisie en `float`.
- `ValueError` pour `2,5` ou `abc` : saisir `2.5` ; gestion robuste des erreurs prévue plus tard.
- `IndentationError` : aligner les blocs conditionnels.
- 449,6 parpaings sans marge : appliquer la majoration avant `ceil`.
- 50 m² de murs bruts au lieu de 44,96 m² nets : déduire la porte.
- 24 m³ au lieu de 3,6 m³ : ne pas confondre hauteur des murs et épaisseur de dalle.
