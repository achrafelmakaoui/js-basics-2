# TD5 — Introduction à JavaScript : Évènements


## 📁 Structure du projet

```
td5-javascript/
├── permutation.html
├── calculatrice-simple.html
├── calcul-IMC.html
└── Calculatrice-Avancee.html
```

---

## Exercice 1 — Permutation

**Fichier :** `permutation.html`

L'objectif est de permuter le contenu de deux zones de texte en cliquant sur un bouton.

### Comment ça marche

On utilise une variable temporaire `temp` pour échanger les valeurs des deux inputs sans en perdre aucune.

```javascript
function permuter() {
    var temp = val1.value;
    val1.value = val2.value;
    val2.value = temp;
}
```

> `temp` conserve la valeur de `val1` le temps que `val1` reçoive celle de `val2`.

---

## Exercice 2 — Calculatrice Simple

**Fichier :** `calculatrice-simple.html`

Une calculatrice qui effectue les 4 opérations de base entre deux nombres.

### Comment ça marche

Chaque bouton appelle une fonction dédiée. On récupère les valeurs des inputs et on affiche le résultat dans un troisième champ.

```javascript
function addition() {
    var nbr1 = document.getElementById("nbr1").value;
    var nbr2 = document.getElementById("nbr2").value;
    result.value = Number(nbr1) + Number(nbr2);
}
```

> Le cast `Number()` est important : sans lui, JavaScript traiterait les valeurs comme des chaînes et les concatènerait au lieu de les additionner.

---

## Exercice 3 — Calcul IMC

**Fichier :** `calcul-IMC.html`

Calcule l'Indice de Masse Corporelle (IMC) et affiche une interprétation selon les normes OMS.

### Formule utilisée

```
IMC = Poids (kg) / Taille² (m)
```

### Comment ça marche

On calcule l'IMC puis on utilise des conditions `if / else if` pour afficher la catégorie correspondante.

```javascript
function calculerIMC() {
    var IMC = poids.value / (taille.value * taille.value);

    if (IMC > 40) {
        result.textContent = "Obésité morbide ou massive";
    } else if (IMC > 35) {
        result.textContent = "Obésité sévère";
    } else if (IMC > 30) {
        result.textContent = "Obésité modérée";
    } else if (IMC > 25) {
        result.textContent = "Surpoids";
    } else if (IMC > 18.5) {
        result.textContent = "Corpulence normale";
    } else {
        result.textContent = "Insuffisance pondérale (maigreur)";
    }
}
```

### Tableau des tranches IMC (OMS)

| IMC | Interprétation |
|-----|----------------|
| < 18.5 | Insuffisance pondérale (maigreur) |
| 18.5 à 25 | Corpulence normale |
| 25 à 30 | Surpoids |
| 30 à 35 | Obésité modérée |
| 35 à 40 | Obésité sévère |
| > 40 | Obésité morbide ou massive |

---

## Exercice 4 — Calculatrice Avancée

**Fichier :** `Calculatrice-Avancee.html`

Une calculatrice scientifique complète avec fonctions trigonométriques, logarithmes, constantes et support clavier.

### Comment ça marche

L'expression tapée est stockée dans une variable `expression`. À chaque clic, on met à jour l'affichage. Quand on appuie sur `=`, on évalue l'expression avec `eval()`.

### Fonctions principales

| Fonction | Rôle |
|----------|------|
| `addToDisplay(char)` | Ajoute un caractère à l'expression |
| `clearDisplay()` | Efface tout (bouton CE) |
| `addConstant('pi'/'e')` | Insère la valeur réelle de π ou e |
| `applyFunc(func)` | Calcule `ln`, `log`, `√`, `x²`, `EXP` |
| `applyTrig(func)` | Calcule `sin`, `cos`, `tan` en degrés |
| `toggleInv()` | Bascule vers `arcSin`, `arcCos`, `arcTan` |
| `calculate()` | Évalue l'expression complète |

### Extrait — fonction calculate()

```javascript
function calculate() {
    let expr = expression.replace(/\^/g, "**");  // ^ devient ** pour la puissance
    expr = expr.replace(/(\d+)%/g, n => n / 100); // gère le %
    let result = eval(expr);
    expression = String(result);
    updateDisplay(expression);
}
```

### Extrait — fonctions trigonométriques

```javascript
function applyTrig(func) {
    let rad = val * (Math.PI / 180); // conversion degrés → radians
    if (func === "sin") result = Math.sin(rad);
    // ...
}
```
