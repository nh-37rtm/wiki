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
#### Passage par référence
````
let arr1 = [1, 2, 3];

// Passage par référence
let arr2 = arr1;

arr2[0] = 42;

console.log(arr1[0]); // 42 
console.log(arr2[0]); // 42 
````

#### Spread & Rest(ructuring)

````javascript
function add(...numbers) { // REST !
  console.log(numbers);
}

add(1, 2); // [1, 2]
add(1, 2, 3); // [1, 2, 3]
add(1, 2, 3, 4); // [1, 2, 3, 4]


// const = même portée que le let, mais il m'interdit de modifier la référence de la variable
const arr1 = [1, 2];
const arr2 = [3, 4];

// const arr3 = [arr1, arr2]; // [1, 2, 3, 4]
// console.log(arr3); // [[1, 2], [3, 4]] // PAS BON !

const arr3 = [...arr1, ...arr2]; // SPREAD
console.log(arr3); // [1, 2, 3, 4]

// A noter que spread fonctionne de la même manière pour les objets
const obj1 = {
  a: 1,
  b: 2
};

const obj2 = {
  c: 3,
  d: 4,
  a: 42 // a VA ETRE SURCHARGEE
}

const obj3 = {...obj1, ...obj2};

console.log(obj3); // {a: 42, b: 2, c: 3, d: 4}
````

#### Destructuration

````
Destructuration de tableau

const resultServer = [1, [2, 3, 4], 5];

/*
let a = resultServer[0];
let b = resultServer[1];
let c = resultServer[2];
let d = resultServer[3];
let e = resultServer[4];
*/

let [a, [b, c, d], e] = resultServer;

console.log(a, b, c, d, e);
````

Destructuration d'objet

````
function direBonjour({firstname, lastname, age = 42}) {
  console.log(`Bonjour ${firstname} ${lastname.toUpperCase()} et j'ai ${age} ans`);
}

// 5000 ligne de code d'écart
direBonjour({lastname: "toto", firstname: "dupond", age: 24});
````

### TypeScript

Typage des données

traduction => transpilatio

Babel le plus puisant mais par defaut google à développer tracer

#### les types

boolean
any

#### les Annotations en AtScript

descriptor => type sur lequel l'annotation à été appliquée


@Component


Un composant contrôle une vue ou une partie d'une vue
- gérer la vue
- gérer l'affichage relative à cette vue

Toute la page est décomposée en composants

hierarchie de composant
route de communication

définition de la hiérarchie par l'utilisation des composants. Un composant qui utilise un autre est le parent 

#### main.ts
- déterminer sur quelle plateforme l'application va tourner
  - appli mobile
  - appli web
  - appli bureau
  
#### app.module.ts
lot de fonctionnalité, au moins un module par application
- permet d'importer des fonctionnalités
- déclaration des composant de l'appli

#### app.component.ts

ex mon-toto.component.ts

bootstrap module => rien a voir avec le framework bootstrap


#### component
selector => identifiant uniqueu du composant
declarations => declare les composant utilisés
template => vue du composant

propriété configurable du composant
à l'aide de @Input pour tagger le nom de la propriété

dans un composant 

la gestion est en 1 way data binding,
la reférence partagée 

La données transite du haut vers le bas (père vers les enfants)

pour notifier dans le sens inverse on peux utiliser une propriété avec @Output avec un nouvel objet EventEmitter()
declencher avec emit

### directive structurelle
modification du dom
#### ngIf
afficher ou en fonction de la valeur de la variable utilisée
peux aller de pair avec le ng-template dans le cas de

```` html
<p *ngIf="name; else noName">
<ng-template #noName>
<p>else</p>
</ng-template>
````


#### ngFor
````html
<p *ngFor="let ch of tab; let i = index; let isFirst = first; let isLast = last">
 N° {{i+1}}
  - {{ch}}
  <span class="delete" (click) => "removeString(i)" >(delete) </span>
  <b *ngIf="isFirst">Je suis le premier !!</b>
  <b *ngIf="isLast">Je suis le dernier !!</b>

</p>
````
https://guide-angular.wishtack.io/angular/composants/ngfor
https://angular.io/api/common/NgForOf
Télécharger XXX.Instructions_CLI.pdf (238.06 KB)
https://angular.io/api/common/NgSwitchCase


### Composants

## Dumb
Dumb => silencieux

## smart

Data Driven component
niveau de granularité fort pour délégation au père

### Dependecy injection

Partage une instance (Pas un Singleton) à travers l'enssemble des composants

chaque composant à sont injecteur, si il ne trouve pas le provider convenable il demande à l'injecteur de parent
@Injectable est relié à l'injecteur racine par defaut

logique de cloisonement pour les injecteur pour eviter garder un minimum d'instance injectable

utiliser la propriété ``providers`` pour associer un provider

Une DI peux en injecteur une autre

### Promeses & Observable

#### Promesses 
Pyramid of doom (imbrication de callback en formant une pyramide) => réponse les promesses ou promises

````javascript
// Entité A
function generatePromise() {
  let promise = new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve({
        pommes: 2,
        poires: 4
      });
      //reject("Tout va mal! Le magasin était fermé");
    }, 1000);
  });
  
  return promise;
}

// Entité B
/*generatePromise()
  .then((sacDeCourse) => {
    console.log("Bob réagit à la fin de la promesse");
    console.log(sacDeCourse);
    
    return generatePromise();
  })
  .then((sac) => {
    console.log("COUREUR NUMERO 2");
    console.log(sac);
  
    return generatePromise();
  })
  .then((sac) => {
    console.log("COUREUR NUMERO 3");
    throw new Error('Erreur random');
    console.log(sac);
  
    return generatePromise();
  })
  .then((sac) => {
    console.log("COUREUR NUMERO 4");
    console.log(sac);
  })
  .catch((err) => {
    console.error("Une erreur est survenue");
    console.error(err);
  })
;*/

// Avec async et await !

async function main() {
  let sac = await generatePromise();
  console.log(sac);
  let sac2 = await generatePromise();
  console.log(sac2);
}


main();

console.log("Promesse n'est pas bloquante");
````

voir :
https://blog.macademia.fr/javascript/comprendre-les-promesses-en-javascript

#### Observable

Ex :

Message sur le chat facebook 
- titre change
- son joué
- chat mis à jour

rxjs

````
this._data = new Observable<strint>( observer => {} )
````

TEAR DOWN Logic =>
nnétoyage ou desctructeur


this._data
  .finally()
  .retry()
  ...


### Rxjs
Observable => utilisé pour de multiple échanges
Promesse => utilisé ponctuellement,

il est possible de convertir une Promesse en Observable

### Pipes

traitements dans les templates 
{{ nalme | lowercase | slice:0:5 }}

traitement relatif à la vue

{{observable|async}}
- abonnement
- reccupération valeur
- désabonnement

chaque changement de dom réinterprète l'enssemble de la vue
les pipes utilisent un cache

attribut ``pure`` à false : plus de cache


### Formulaire
#### model driven formulaire
un form group qui inclu plusieurs formulaire
on crées nos form control associé au form group via une clée

observer possible au niveau du changement


#### Custom  validator


Validator.required va
##### synchrone
retour => erreur
null => tout va bien

methode static validate
puis ajouter le validateur au moment du new FormControl

static validateEmail( data: FormControl ) {
  console.log( data.value )
}

##### asynchrone

utiliser comme pour la validateur, mais utiliser le 3 ième argument de new FormControl à la place

utiliser l'interface IValidation pour le validateur

formgroup builder :

https://angular.io/guide/reactive-forms#using-the-formbuilder-service-to-generate-controls

HttpClientModule

### style

voir site codepen


### Debug
variable isDevMod from angular.core
utiliser --prod lors du build pour passer la variable à false

pas de risque pour la prod étant donné que le code non utilisé ne devrai pas apparaitre dans la version de prod (Tree Leaf Shaking)

### guards

https://medium.com/@jacobneterer/angular-authentication-securing-routes-with-route-guards-2be6c51b6a23

### References

Mazen Gharbi
https://codepen.io/
Mazen Gharbi
https://angular.io/api/common/http/HttpInterceptor




### rappel composant

````
template : `<app-child [toto]="valeur"></app-child>
<app-child></app-child>
<app-child></app-child>`

...

@Input("toto") maProprio : string;
````

Dans le composant :

ngOnInit()
ngAfterViewInit()
ngOnDestroy()

Pouruqoi initialiser dans ngOnInit plutôt que dans le constructor ?

constructeur est appellé avant, trop avant, les données ne sont pas toujours initialisées
le constructeur n'est utilisé que pour la gestion des dépendances

migration progressive vers angular possible

pas un injecteur par component sauf quand on surcharge un injecteur on à une nouvelle instance

MomentJs librairie DateTime
librairie Javascript possible de l'utiliser comme une librairie Angular avec un injecteur en template

### modification du dom (@ViewChild)

https://blog.macademia.fr/angular/comprendre-lannotation-viewchild

éviter très fortement d'utiliser document dans le controleur (même si c'est possible)
il est possible de faire du render côté serveur : Server Side Rendering

````
<p #myParagraph>

... modele

@ViewChild('myParagraph') variableCoteModele : ElementRef<HTMLParagraphElement>

onChangeTextCalue() {
  this.variableCoteModele.nativeElement.innerText = "Nouvelle value !";
}
````

### Directives

Certaines action sur les styles par exemple ne doivent pas êtres implémenter côté composant, et les pipes sontlimités
Utilisation des directives

<div appHighLioght color="red">BLABLA</div>

dans le module ...
````
@NgModule(

  directives = [ ... ]
)

@Directive({
  selector : "[appHighlight]"
})

// les crochets sont importants

export class HighlightDirective {
  @Input() color: string;
  @Ooutput() clickElement = new EventEmitter();
  constructor(private _element: ElementRef) {}

    // met à jour la div en changeant la couleur
    @HostListenet("click")
    onClick() {
      this.
      let {nativeElement} = this._element;
      this._element.nativeElement.style.backgroundColor = this_element.nativeElement.style.bacvkgroundColor ?null : "red";
    }
  }
}
````

Un composant est une directive avec de l'embalage :
  - template
  - templateUrl
  - styleUrl

Tout ce qu'il est possible de faire avec un compenent on peux le faire avec une directive

#### deux directives supplementaires

avec des @Input param: string;

<div appDir1 appDir2 [param]="'Toto'">
  BLABLA
</div>

ça passe dans les deux directive, l'ordre de définition dans le div semble important, mais en fait non.
l'ordre viens de l'ordre de la définition dans le module

Pour le Output() onclick = new EventEmitter(); le père réagit aux deux EventEmitter

### Routing

Une vue ou page Angular est régie par un composant, une Url par composant
#### Comment configurer l'appli pour faire le mapping avec les URL  ?

Le changement est toujours fait côté front, jamais côté back

ajouter le module RouterModule.forRoot(APP_ROUTES, {useHash : false})

APP_ROUTES est définit dans un autre fichier ``app.routes.ts`` qui contient 
export APP_ROUTES = [
   component : LoginComponent ,
   path: 'login' // pas de '/' au debut
  }
  ...
  { refirectTo: '/login',
   path : '**'
  }
]

hashbang permet pour la compatibilité < html5

useHash:false

Simplement en faisant ça des pages blanches s'affichent, car nous n'avons pas défini les zones dynamiues

#### Comment définir une zone de contenu dynamique ?

<router-outlet></router-outlet>

de cette façon: 
````html
<ul>
<li>
  <a href="/contact">Contact</a>
</li>
<li>
  <a href="/contact">Contact</a>
</li>
</ul>````

on recharge toute la page, utiliser 
````html
<a [routerLink]="['/home']">Home</a>
````

zone dynamique contenant zone dynamique et zone statique

le routing outlet peux intégrer d'autres routing outlet ce qui permet de gérer une hierarchie de routing outlet

ceéation de deux composants, avec routage,

avec un home.routes.ts

utiliser :   dans la définition principale parente 
children: [
      { path: '', redirectTo: 'overview', pathMatch: 'full' },
      { path: 'overview', component: Overview },
      { path: 'specs', component: Specs }
    ]


### Parametres dans routes

````
// injection
constructor(private activatedRoute: ActivatedRoute) {}

ngOninit() {
  this.valueToDisplay = this.activatedRoute.snapshot.params.id:
  // id etant le nom de la variable


// parametre variable quand on n'est dans le init  
this.activatedRoute.params.subscribe( params => {
  this.valueToDisplay = params.id
})

}

````

### Lazy loading

défaut du one page 
- grosse partie/grosse partie, tout sera chargé et donc pas optimisé

association page => module

au moment du rooting

path: 'opportunities',
loadChildren: () => import( '/lazy/lazyModule' ).then( (m) => m.LandingModule )

ne pas utiliser Module.forRoot mais Module.forChild

### Gardien

utilisation de l'interface CanActivate (methode canActivate())

la vrai sécurité n'est pas côté client mais côté serveur.
le gardien va permetre de garder une cohérence

canDeactivate va permetre d'éviter la perte de données cf. le êtes vous sur de vouloir quiter la page sans sauvegarder ?


### tests unitaires

librairies :
- Jasmine : enclenche les tests unitaires (équilent JUnit)
- Karma : résultat visuel des tests unitaires
````
ng test
````

 #### line coverage

````
ng test --line-coverage
````

karma.conf.js permet de définir les poucentages de line coverage

describe => thématique

expect(calculator.calculate('3 * 3')).toEqual(9)

Pour tester les entités engular :

Utiliser un module de test
beforeEach permet d'initialiser chaque test
partir de TestBed

TestBed.configureTestingModule( {
  imports: [CalculatorModule]
})

beforeAll, ne remet pas à zero les instances

#### Test de component

fixture surcouche de test à component
TestBed.createComponent(HelloComponent)
fixture.component.name = 'John'
fixture.
expect(ficture.debugElement.nativeElement.innerText).toEqual('Hello John!')

#### F.I.R.S.T

- Fast
- Independant
- Repeatable : résultat ne dépent pas du nombre d'execution
- selfChecking : PAs d'intervention humaire
- Timely : pertinence du test


#### Test Long

ajouter un done()
fakeAsync() => {

};
tick va accélerer le temps

#### mock

jamine.SpyObj<>

lancer un done() pour indiquer la fin d'un test asynchrone

#### test e2e
Webdriver, Sélénium => Protractor

### exercice

edition et ajout de tiquet : même composant
R.O  pour gerer Login + Home

### Conclusion

- Il reste beaucoup et la formation était dense, 
- Il est possible d'utiliser des outils comme Redux
- il manque la pratique, le but est de gagner en productiviter
- Garder en tête le séparation of concern
- la modularité est la pierre angulaire
  

tout à fait d'accord sur le point de faire de
plus petits pas dans l'exercice, mais fil rouge est bien pour 
rappels javascript j'etais d'accord
accès aux env du live coding : super


