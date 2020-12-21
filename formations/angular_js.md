# Intro
## Angular

c'est un framework et pas simplement une librairie :
- lourdeur
- mais puissance

LiveCoding

Tour de table 3 points : 

- déjà développé  en quel language ?
- problématique
- problématiques et performances


``Angular JS`` complète refonte avec ``Angular``

Single page application, ne change pas de page à chaque fois => tout l'application est chargée au démarrage.

Angular 2 => Angular 
- plus de JQuery

Angular 1.x => Angular JS

MV VM

Modularité très importante en Angular JS
``Plus on développe, moins on a besoin de développer``

Pourquoi update Angular JS vers Angular ? à cause de la performance en priorité

## Javascript
1997 unification du language pour les navigateurs avec le standard 

Microsoft => JScript
EcmaScript => Oracle, EcmaScript

1997 => 2009 pas de mise à jour du moteur javascript
Google reprend les rènes avec V8

- Dynamiquement typé
- faiblement typé
  
null => le développeur decide de la valeur
undefine => subit, le moteur positinne

### Objet
var user = {
  firstname: 'Joe',
  lastname: 'Dupond',
  age: 41,
  porteFeuille: {
    porteCarte: {
      carteBleue: true
    }
  }
};

````javascript
console.log(user.firstname); // Joe

// Ajout / Edition / Suppression dynamique
user.taille = 180;
user.age++;

delete user.lastname;

// Accéder à la valeur carteBleue 
console.log(user.porteFeuille.porteCarte.carteBleue); // true
console.log(((user.porteFeuille).porteCarte).carteBleue); // true

console.log(user.proprieteNonExistante); // undefined
console.log(user.proprieteNonExistante.autrePropriete); // ERREUR !
````

### Tableaux
````
var tab = [1, 2, "trois", true]; // Tableau déclaré et initialisé
// Taille du tableau
console.log(tab.length); // 4

tab.push(4); 
console.log(tab); // [1, 2, "trois", true, 4]

tab[1] = "deux modifié";
console.log(tab); // [1, "deux modifié", "trois", true, 4]

tab.splice(2, 1); // Retirer le "trois"
console.log(tab); // [1, "deux modifié", true, 4]
````

### autres
EcmaScript 2015 nouvelle méthodologie
Linter => sonar pour les IDE
get / set pour passer par les properties plutôt que directement par les propriété

egalités en javascript :
https://dorey.github.io/JavaScript-Equality-Table/

éviter d'oublier les point virgules


````javascript
// AEL - Automatic End of Line
console.log(1)
console.log("Bonjour")

var a = 2
console.log(a)

function toto() {
  return // AEL -> return;
    42;
}
````

#### classes

console.log(toto()); // undefined
propriété privée => prefixe démarre par _

toujours utiliser let, le transpileur intégré va se charger de la rétro compatibilité

toujours implémenter les Arrow function pour les callbacks

````javascript
// Standard
function add(a, b) {
  return a + b;
}

// Arrow function
let addArrow = (a, b) => a + b;

let addArrow = (a, b) => {
  let result = a + b;
  return result;
}

console.log(add(1, 2));
console.log(addArrow(1, 2));
````

#### Template strings

utilisation du backquote qui va permetre d'intégrer les saut de ligne

````
let a = 1;
let templateStr = `Bonjour tout le monde ${a}

Passage à la ligne`;

console.log(templateStr);
````

#### Spread & Rest



