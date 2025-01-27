
# Programmation Orientée Objet (POO) en PHP : Une Introduction Complète

## Introduction à la POO

La Programmation Orientée Objet (POO) est un paradigme de programmation qui structure le code autour des objets, qui sont des instances de classes. En PHP, la POO permet de mieux organiser le code, de le rendre modulaire, réutilisable et maintenable.

### Concepts Clés de la POO

-   **Classe** : Un modèle définissant les propriétés et les méthodes communes à un objet.
-   **Objet** : Une instance de classe.
-   **Attributs** : Les variables définies dans une classe (propriétés d'un objet).
-   **Méthodes** : Les fonctions définies dans une classe (comportements d'un objet).
-   **Encapsulation** : Restreindre l'accès direct à certains éléments d'une classe.
-   **Héritage** : Permettre à une classe de dériver d'une autre.
-   **Polymorphisme** : Permettre à différentes classes d'être traitées uniformément à travers une interface commune.

## Syntaxe de Base de la POO en PHP

### Définir une Classe et Créer un Objet

```php
<?php
class Personne {
    public $nom;
    public $age;

    public function __construct($nom, $age) {
        $this->nom = $nom;
        $this->age = $age;
    }

    public function sePresenter() {
        return "Je m'appelle {$this->nom} et j'ai {$this->age} ans.";
    }
}

// Instanciation d'un objet
$personne = new Personne("Alice", 30);
echo $personne->sePresenter();
?>

```

### Les Modificateurs d'Accès

-   **public** : Accessible partout.
-   **protected** : Accessible dans la classe et ses sous-classes.
-   **private** : Accessible uniquement dans la classe.

Exemple :

```php
<?php
class Exemple {
    public $publicAttr = "Public";
    protected $protectedAttr = "Protected";
    private $privateAttr = "Private";

    public function afficherAttributs() {
        echo $this->publicAttr;
        echo $this->protectedAttr;
        echo $this->privateAttr;
    }
}

$exemple = new Exemple();
echo $exemple->publicAttr; // Fonctionne
//$exemple->protectedAttr; // Erreur
//$exemple->privateAttr;   // Erreur
?>

```

### Héritage

L'héritage permet de créer une nouvelle classe basée sur une classe existante.

```php
<?php
class Animal {
    public function marcher() {
        return "Je marche.";
    }
}

class Chien extends Animal {
    public function aboyer() {
        return "Je aboie.";
    }
}

$chien = new Chien();
echo $chien->marcher();
echo $chien->aboyer();
?>

```

### Polymorphisme avec Interfaces et Classes Abstraites

#### Interface

Une interface définit un ensemble de méthodes qu'une classe doit implémenter.

```php
<?php
interface Vehicule {
    public function demarrer();
    public function arreter();
}

class Voiture implements Vehicule {
    public function demarrer() {
        return "La voiture démarre.";
    }

    public function arreter() {
        return "La voiture s'arrête.";
    }
}
?>

```

#### Classe Abstraite

Une classe abstraite peut contenir des méthodes implémentées ou non (méthodes abstraites).

```php
<?php
abstract class Forme {
    abstract public function calculerAire();
}

class Carre extends Forme {
    private $cote;

    public function __construct($cote) {
        $this->cote = $cote;
    }

    public function calculerAire() {
        return $this->cote * $this->cote;
    }
}
?>

```

## Bonnes Pratiques

1.  **Respectez les conventions de nommage** : Utilisez le PascalCase pour les noms de classes.
2.  **Utilisez l'autoloading** : Pour charger automatiquement les classes.
    
    ```php
    spl_autoload_register(function ($class) {
        include $class . '.php';
    });
    
    ```
    
3.  **Favorisez la composition à l'héritage** : Réutilisez le code en combinant des objets plutôt qu'en héritant.
4.  **Protégez vos données** : Utilisez les modificateurs d'accès appropriés.

## Exemple Complet : Système de Gestion d'une Bibliothèque

### Structure des Fichiers

```
librairie/
├── index.php
├── classes/
│   ├── Livre.php
│   ├── Auteur.php
│   └── Bibliotheque.php

```

### Code des Classes

#### Livre.php

```php
<?php
class Livre {
    private $titre;
    private $auteur;

    public function __construct($titre, Auteur $auteur) {
        $this->titre = $titre;
        $this->auteur = $auteur;
    }

    public function getDescription() {
        return "{$this->titre} par {$this->auteur->getNom()}";
    }
}
?>

```

#### Auteur.php

```php
<?php
class Auteur {
    private $nom;

    public function __construct($nom) {
        $this->nom = $nom;
    }

    public function getNom() {
        return $this->nom;
    }
}
?>

```

#### Bibliotheque.php

```php
<?php
class Bibliotheque {
    private $livres = [];

    public function ajouterLivre(Livre $livre) {
        $this->livres[] = $livre;
    }

    public function afficherLivres() {
        foreach ($this->livres as $livre) {
            echo $livre->getDescription() . "\n";
        }
    }
}
?>

```

### Point d'Entrée : index.php

```php
<?php
require_once 'classes/Livre.php';
require_once 'classes/Auteur.php';
require_once 'classes/Bibliotheque.php';

$auteur = new Auteur("Victor Hugo");
$livre = new Livre("Les Misérables", $auteur);

$bibliotheque = new Bibliotheque();
$bibliotheque->ajouterLivre($livre);
$bibliotheque->afficherLivres();
?>

```

# Les Variables et Comparaisons en PHP

## Les Variables en PHP

En PHP, une variable est représentée par un signe `$` suivi d'un nom. Les noms de variables sont sensibles à la casse.

### Déclaration et Initialisation
```php
$nom = "John";
$age = 30;
$estConnecte = true;
```

### Types de Variables
PHP est un langage faiblement typé, ce qui signifie que vous n'avez pas besoin de déclarer le type d'une variable explicitement. Cependant, il existe plusieurs types de données principaux :

#### 1. Types Scalaires
- **String (Chaîne de caractères)**
  ```php
  $texte = "Bonjour, le monde!";
  ```

- **Integer (Entier)**
  ```php
  $nombre = 42;
  ```

- **Float (Nombre à virgule flottante)**
  ```php
  $decimale = 3.14;
  ```

- **Boolean (Booléen)**
  ```php
  $estVrai = true;
  $estFaux = false;
  ```

#### 2. Types Composés
- **Array (Tableau)**
  ```php
  $tableau = ["pomme", "banane", "cerise"];
  ```

- **Object (Objet)**
  ```php
  class Personne {
      public $nom;
      public $age;
  }

  $personne = new Personne();
  $personne->nom = "Alice";
  $personne->age = 25;
  ```

- **Callable (Appelable)** : Fonction ou méthode appelée dynamiquement.
  ```php
  function saluer($nom) {
      return "Bonjour, $nom!";
  }

  $appel = 'saluer';
  echo $appel("Alice");
  ```

- **Iterable (Itérable)** : Un objet ou tableau traversable avec une boucle.

#### 3. Types Spéciaux
- **NULL** : Absence de valeur.
  ```php
  $variable = null;
  ```

- **Resource** : Référence à une ressource externe (fichier, connexion à une base de données, etc.).

### Vérification des Types
- **gettype()** : Retourne le type d'une variable.
  ```php
  echo gettype($age); // integer
  ```

- **var_dump()** : Affiche le type et la valeur d'une variable.
  ```php
  var_dump($decimale); // float(3.14)
  ```

### Conversion de Type
PHP permet de convertir une variable d'un type à un autre :
```php
$nombre = (int) "42"; // Convertit une chaîne en entier
$texte = (string) 123; // Convertit un entier en chaîne
```

## Opérateurs de Comparaison

Les opérateurs de comparaison permettent de comparer des valeurs. Voici les principaux opérateurs disponibles en PHP :

### 1. Comparaison Simple
- **Égalité** : `==`
  ```php
  $resultat = (5 == "5"); // true (valeurs égales)
  ```

- **Différence** : `!=` ou `<>`
  ```php
  $resultat = (5 != "6"); // true
  ```

- **Inférieur** : `<`
  ```php
  $resultat = (3 < 5); // true
  ```

- **Supérieur** : `>`
  ```php
  $resultat = (7 > 4); // true
  ```

- **Inférieur ou égal** : `<=`
  ```php
  $resultat = (5 <= 5); // true
  ```

- **Supérieur ou égal** : `>=`
  ```php
  $resultat = (10 >= 8); // true
  ```

### 2. Comparaison Strictement Typée
- **Identité stricte** : `===`
  ```php
  $resultat = (5 === "5"); // false (types différents)
  ```

- **Différence stricte** : `!==`
  ```php
  $resultat = (5 !== "5"); // true
  ```

### 3. Comparaison Spéciale
- **Spaceship (vaisseau spatial)** : `<=>`
  Retourne :
  - `-1` si la première valeur est inférieure,
  - `0` si elles sont égales,
  - `1` si elle est supérieure.

  Exemple :
  ```php
  echo 5 <=> 10; // -1
  echo 10 <=> 10; // 0
  echo 15 <=> 10; // 1
  ```

### 4. Opérateurs Logiques
- **ET** : `&&` ou `and`
  ```php
  $resultat = (true && false); // false
  ```

- **OU** : `||` ou `or`
  ```php
  $resultat = (true || false); // true
  ```

- **NON** : `!`
  ```php
  $resultat = !true; // false
  ```

- **XOR** : `xor`
  ```php
  $resultat = (true xor false); // true
  ```

## Vérifications avec des Fonctions Utilitaires

### Fonctions de Test de Type
- **is_int()** : Vérifie si la variable est un entier.
- **is_float()** : Vérifie si la variable est un flottant.
- **is_string()** : Vérifie si la variable est une chaîne.
- **is_bool()** : Vérifie si la variable est un booléen.
- **is_array()** : Vérifie si la variable est un tableau.
- **is_object()** : Vérifie si la variable est un objet.
- **is_null()** : Vérifie si la variable est `null`.

Exemple :
```php
$variable = "Hello";
if (is_string($variable)) {
    echo "C'est une chaîne de caractères.";
}
```

### Fonctions de Comparaison
- **empty()** : Vérifie si une variable est vide (valeur équivalente à `false`).
  ```php
  $vide = "";
  if (empty($vide)) {
      echo "La variable est vide.";
  }
  ```

- **isset()** : Vérifie si une variable est définie et n'est pas `null`.
  ```php
  $nom = "Alice";
  if (isset($nom)) {
      echo "La variable est définie.";
  }
  ```
Ajoutons d'autres notions syntaxiques et pratiques pour enrichir votre documentation PHP :

---

# Complément de Syntaxe et Concepts en PHP

## 1. Les Constantes

Les constantes sont des valeurs définies une fois pour toutes, accessibles partout dans le script.

### Déclaration
```php
define("NOM_CONSTANTE", "Valeur");
const AUTRE_CONSTANTE = 123;
```

### Utilisation
```php
echo NOM_CONSTANTE; // Affiche "Valeur"
```

---

## 2. Structures de Contrôle

### Conditions
```php
if ($a > $b) {
    echo "a est plus grand que b";
} elseif ($a == $b) {
    echo "a est égal à b";
} else {
    echo "a est plus petit que b";
}
```

### Switch
```php
$couleur = "rouge";

switch ($couleur) {
    case "bleu":
        echo "La couleur est bleu";
        break;
    case "rouge":
        echo "La couleur est rouge";
        break;
    default:
        echo "Couleur inconnue";
}
```

---

## 3. Boucles

### While
```php
$i = 1;
while ($i <= 10) {
    echo $i;
    $i++;
}
```

### For
```php
for ($i = 0; $i < 5; $i++) {
    echo $i;
}
```

### Foreach
```php
$fruits = ["pomme", "banane", "cerise"];
foreach ($fruits as $fruit) {
    echo $fruit;
}
```

---

## 4. Les Fonctions

### Déclaration
```php
function addition($a, $b) {
    return $a + $b;
}

echo addition(5, 3); // Affiche 8
```

### Valeur par Défaut
```php
function salutation($nom = "Utilisateur") {
    echo "Bonjour, $nom!";
}

salutation(); // Affiche "Bonjour, Utilisateur!"
```

---

## 5. Gestion des Erreurs et Exceptions

### Try-Catch
```php
try {
    if ($a < 0) {
        throw new Exception("Valeur négative non autorisée");
    }
} catch (Exception $e) {
    echo "Erreur : " . $e->getMessage();
}
```

---

## 6. Inclusion de Fichiers

### `include` et `require`
```php
include "fichier.php";  // Affiche une alerte en cas d'erreur
require "fichier.php";  // Génère une erreur fatale en cas d'échec
```

---

## 7. Opérateurs Avancés

### Opérateur Ternaire
```php
$resultat = ($a > $b) ? "a est plus grand" : "b est plus grand";
```

### Null Coalescing
```php
$valeur = $variable ?? "Valeur par défaut";
```

---

## 8. Manipulation de Chaînes

### Concaténation
```php
$texte = "Bonjour" . " " . "le monde!";
```

### Interpolation
```php
$nom = "Alice";
echo "Bonjour, $nom!";
```

---

## 9. Superglobales

- **`$_GET`** : Récupère les données envoyées via une URL.
- **`$_POST`** : Récupère les données d’un formulaire.
- **`$_SESSION`** : Stocke les données pour une session utilisateur.
- **`$_COOKIE`** : Accède aux cookies.
- **`$_SERVER`** : Informations serveur et d'exécution.

---

## 10. Classes Anonymes
```php
$objet = new class {
    public function saluer() {
        return "Salut!";
    }
};

echo $objet->saluer(); // Affiche "Salut!"
```
