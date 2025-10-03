## Les types

Il existe 3 **principaux** type par défaut :

- `char` : un caractère qui est défini entre des "single-quotes" (`'`). Il faut aussi se rappeler qu'un `caractère` est plus précisement un `u_int8_t`, c'est a dire un nombre entier non signé (seulement positif). Il est donc possible de le traiter comme un chiffre.
- `int` : un nombre entier.
- `float` : un nombre a virgule.

## Les variables

La déclaration d'une variable s'effectue comme ceci :  
`[type de variable] [nom de variable];`  
comme par exemple  
`int nombre;`

Pour assigner une valeur à une variable :  
`[type de variable] [nom de variable] = [valeur];`

A noter que le type de la variable doit correspondre à la valeur (et vice versa).

Exemple avec les 3 types de variables vu précédemment :

```c
int nombre = 10;
float nombre_a_virgule = 3.14;
char lettre = 'B';
```

## Les listes (ou tableaux comme dit le prof)

Les listes servent à avoir plusieurs valeur différentes au sein d'une même variable. Elle sont similaire à la déclaration d'une variable, mais avec l'ajout des crochets `[]`. Une liste à une taille fixe, qui peut être déterminer automatiquement par le programme si elle est assigner dès le départ. Sinon, ce sera à l'utilisateur de spécifier la taille entre les crochets :

```c
int ma_liste[]; 
/* 
ne marche pas car elle n'est pas initialisée,
et sa taille n'est pas spécifié.
*/


int ma_nouvelle_liste[26]; 
/*
marché, la liste est pas initialisée, 
mais sa taille est spécifiée. 
*/


int encore_une_autre_liste[] = {1, 2, 3}; 
/* 
la liste est initialisé mais sa taille n'est pas
spécifiée, elle est donc déduite automatiquement
et est de 3 (car il y a 3 éléments dans la liste)
*/


int je_jure_cest_la_derniere_liste[5] = {1, 2, 3}; 
/* 
ici, la taille et la valeurs sont preciser, 
la liste comporte 5 nombre, 
avec les 3 premier étant définit.
*/
```

On peut accéder aux éléments d'une liste de taille $n$ avec l'emplacement de la première valeur étant $0$ et l'emplacement de la dernière valeur étant de $n-1$.

```c
int liste[] = {1, 2, 5};
liste[0]; // 1
liste[1]; // 2
liste[2]; // 5
liste[3]; // erreur la liste est trop courte
```

---
&nbsp;

## Formatage des types

- `%s` : `string`, pour afficher une suite de caractère.
- `%d` : `decimal (number)` pour afficher un nombre entier **positif**.
- `%f` : `float` pour afficher un nombre à virgule (flottante).
- `%c` : `character` pour afficher un caractère.

## Caractères spéciaux

Il existe plusieurs caractère spéciaux, qui permette de manipuler l'apparence du terminal.

- `'\n'` : `newline`, insert a retour a la ligne.
- `'\t'` : `tab`, fait une tabulation (espace de 4-8 caractère).
- `'\\'` : écrire `\` dans le terminal.

## Interaction avec l'utilisateur

Pour interagir avec l'utilisateur, C dispose de `libraries` (ou `bibliothèques` en français) permettant d'afficher du texte dans la console, ou de permettre à l'utilisateur à entrer du texte.  
La bibliothèque principale est `stdio. h`, et `conio.h` (qui elle a été fournit par l'établissement, et ne fait pas partie de C par défaut).

Les fonctions les plus connues sont `printf` et `scanf`.

### `printf`

Utilisation :  
```
printf( [string/suite de caractères] );
printf( [suite de caractère possédant au moins 1 element de formatage], [ variables (séparer par des virgules s'il y'en a plusieurs) ]);
```

```c
printf("Bonjour") // écrit Bonjour dans la console
printf("Bon%s", "jour") // écrit Bonjour (a noté que `%s` s'est fait remplacer par "jour")
printf("%s", 23); // erreur pas cool
```

Il est impératif d'utiliser un formatage afin d'afficher une variable :

```c
int nombre = 18;

printf(nombre); // NON

printf("%d", nombre); // ouiii
printf("%d", 23); // ouiiii
printf("Année : %d, mois : %d, jour : %d", 2020, 10, 13);
```

### `scanf`

La fonction `scanf` permet a l'utilisateur de saisir une valeur. Elle prend 2 arguments, le premier étant le formatage et le deuxième la variable dans laquelle stocker la valeur entrée par l'utilisateur.  
La variable est obligatoirement précédé par `&` (on ignorera sa fonction pour le moment).

```c
int nombre;

scanf("%d", &nombre);
/*
la valeur entrée par l'utilisateur est converti
en un chiffre par le formatage de %d,
et est stocker dans la variable nombre.
*/


scanf("%s", &nombre); 
/* 
on be peut pas mettre une suite de caractère
dans une variable censé contenir un nombre.
*/
```

***ATTENTION** : il faut appuyer sur ENTRER pour valider la saisie.*

### `getche`

La fonction `getch` vient de la *library* `conio.h`. Elle permet à l'utilisateur d'entrer 1 caractère a la fois, sans avoir a appuyer sur ENTRER.

```c
char c;
c = getche();

// utilisateur tape 'A'
// c = 'A'
```

---
&nbsp;

## Les opérations mathématiques

Les expressions mathématique sont généralement les même en programmation et en classe.

```c
int i = 3 + 2; // i = 5

i = 3; // i = 3
i++; // i = i + 1
i--; // i = i - 1
i += 1; // i = i + 1
i -= 1; // i = i - 1
i *= 3; // i = i * 3
i /= 3; // i = i / 3
```

Pour les calcules plus complexe tel que la racine carré, les fonctions cosinus, et exposants, on utilisera la *library* `math.h`. Il n'est pas nécessaire de le savoir pour le DS (sauf si le prof est pas gentil).

## Les opérations logiques

Les opération logique sont similaires au porte logique étudiées avec M.&nbsp;Perronin. Elles permettent la manipulation de bit (un peu de sérieux svp). 

(Vous voulez vraiment pas voir ça, et ça nous sert a rien pour mardi donc on s'en tape)

---
&nbsp;
## Les boucles (loop)

### `for loop`

La boucle `for` est utilisé lorsque le nombre d'itération (répétition) est connu à l'avance.  
Elle est divisé en trois partie:  
`for ( [variable]; [condition]; [mise a jour de la condition] )`

La première partie `[variable]` n'est pas obligatoire, si cette même variable est déclarée a l'avance.

```c
for (
    int i = 0; // initialisation de la variable i
    i < 10; // condition
    i++ // mise a jour de la variable
    ) {
        // contenue de la boucle
    }
```

Ce code est similaire à :

```c
int i = 0;

for (
    ; // <- a ne pas oublier de mettre le point virgule seul
    i < 10; // condition
    i++ // mise a jour de la variable
    ) {
        // contenue de la boucle
    }
```

*Il est important de noter que la variable doit être initaliser, c'est a dire avoir une valeur tel que `0`.*


| Valeur de $i$ | Condition | Mise a jour de la valeur | Nombre d'itération (et valeur atteinte par $i$) |
| --- | --- | --- | --- |
|i = 0|i < 3| i++ | `3 itération`, `i final = 2`, `0 1 2`|
|i = 2|i < 4| i++| `2 itération`, `i final = 3`, `2 3`|
|i = 0|i <= 3| i++ |`4 itération`, `i final = 3`, `0 1 2 3`|
|i = 0|i <= 4| i+=2 |`3 itération`, `i final = 3`, `0 2 4`|
|i = 10|i > 3| i-- |`6 itération`, `i final = 3`, `0 1 2 3`|

### `while loop`

Contrairement aux `for loop`, la `while loop` est constitué d'une seul partie: la condition. Elle est utiles lorsqu'on ne connait pas le nombre d'itération a effectuer à l'avance.

`while ( [condition] )`

En revanche, cela implique que la condition soit mise à jour manuellement.

```c
int i = 0;
while (i < 10) {
	printf("%d", i);
	i++;
}
```

Ici, celà revient a faire une `for loop`, mais c'est pour l'exemple.

### `do while`

C'est comme le `while loop` sauf que il y a a minima 1 itération (la condition n'est pas vérifier avant).

```c
do {
	printf("salut mec");
} while (0); // condition toujours fausse, aucune ré-iteration
```

---
&nbsp;

## Les conditions

Les conditions ont un état binaire : `0` ou `1`, Vrai ou Faux.
En réalité, une condition est vrai si elle est égal a autre chose que `0`.

```
1 < 2 // c vrai ca
1 > 2 // c faux ca
```

On utilise le symbole double-égal `==` afin de comparer l'égalité entre deux valeurs. Le symbole `!=` signifie *n'est pas égale à*.

```
1 == 1 // oui
1 == 2 // non t con

1 != 1 // non
1 != 2 // oui
```

### Liaisons de multiples conditions

Pour réunir plusieurs conditions, il existe 2 opération : `&&` qui signifie `ET`, comme la porte logique `AND`, et `||` signifiant `OU`, comme la porte logique `OR`.

```c
(du faux code (encore))
i = 2
condition : i < 3 && i > 0 
/*
i < 3 = vrai
i > 0 = vrai
condition = vrai
*/

condition : i < 3 || i > 5
/*
i < 3 = vrai
i > 5 = faux
condition = vrai
*/
```

### `if, else if, else`

Pour vérifier une condition, on utilise le mot clé `if`.
Un `else if` ou `else` doivent impérativement suivre un `if`.
`else` inclut toutes les situations non testées, il n'y a pas besoin de spécifier une condition. 

```c
int i = 0;
if ( i == 3) {
	// 0 n'est pas égal a 3, donc le code ici ne sera jamais atteint
} else {
	// ici c'est atteint
}
```

```c
int i = 0;
if ( i == 3) {
	// 0 n'est pas égal a 3, donc le code ici ne sera jamais atteint
} else if ( i == 0 ){
	// ici c'est atteint
} else {
	// pas ici, puisque le condition a été validé précédemment dans le else-if
}
```

### Complément sur le `else if`

Puisque pour certains, le `else if` peut parraitre inutile, je vais montrer avec un diagrame son utilité.

```
if (condition) {}
if (autre condition) {}
```

N'équivaut pas à :

```
if (condition) {}
else if (autre condition) {}
```

![very very very 1.png](:/6cc0eb39d09347deb6bda55b9bcf15ab) 

![very very very 2.png](:/4c6ab669bffc4c8eb34b0fe2cef22dea)

C'est a dire, avec de multiple condition en `else if`, dès lors qu'une condition est remplie, le reste des condition qui suivent sont ignorées.

---
&nbsp;
## Les fonctions

Les fonctions permette d'organiser son code et d'éviter les répétitions de logique.
Les fonctions sont structurer comme cela :
```
[type de retour] [nom de fonction]( [paramètres] ) {
	[logique a l'intérieur de la fonction]
}
```

Exemple :

```c
int ajouter(int n1, int n2) {
	return n1 + n2
}
```

Ici, on a définit `int` devant la fonction car nous retournons le produit de `n1` et `n2`. `n1` et `n2` sont des paramètres, c'est à dire, des valeurs qui vont être utilisé dans la fonctions. 
Pour l'utiliser :
```c
int produit;
int a = 3;
int b = 4;

produit = ajouter(a, b); // 7
// ajouter(3, 4) revient a faire pareil.
```

Cas d'erreur :
```c
produit = ajouter(3, 4.0); // n2 est un int (nombre entier), donc on ne peut pas utiliser une chiffre a virgule.
```

### Les fonctions `void`

Certaines fonctions ne vont pas retourner de valeurs, celle ci générallement servent seulement a afficher quelque chose. Pour spécifier qu'on ne veut pas que la fonction renvoie une valeurs, on la spécifie avec le mot `void` comme son type.

```c
void afficher_age(int age) {
	printf("Vous avez %d", age);
}
```

### Notes importantes

#### Variables dans les fonctions

Les variables définit dans une fonction ne sont pas accessible en dehors : 
```c

int ajoute_1(int nombre) {
	int nouveau_nombre = nombre + 1;
	return nouveau_nombre;
}
```
```c
int nombre = ajoute_1(3);
printf("%d", nouveaux_nombre); // marche pas, nouveaux_nombre est une variable seulement existante dans la fonction ajoute_1
```

#### Fonction `main`

La fonction `main` est le point de départ d'un programme. Cela signifie que seul son contenu sera réelement éxecuter.

```c
void afficher_un_truc() {
	printf("un truc");
}

int main(){}
```
*Rien ne se passera car la fonction `main` est vide*

#### Définition d'une fonction

Une fonction ne doit pas être définie autre par que la racine du fichier (hors d'une autre fonctions).

```c

int main() {
	void ma_fonction() {} // non frr fait pas ca
}
```

---
&nbsp;

## Rappel sur l'organisation d'un programme

### `;`
Les points-vigules doivent être utilisé en fin d'action (déclaration d'une variable, opération mathématique, etc).

```c
int i = 0; //correct
void ma_fonction() {}; // ca sert a rien mais c'est pas grave pour autant
```

### `{}`

Les accolades sont utilisées lorsqu'une action a un *corps* (*body* en anglais), c'est à dire plusieurs action relié a un terme (tel qu'une boucle, une fonction ou une condition). Il est inutile de mettre un point-virgule derrière la fermeture du *body* tel ceci : `...{...}; // <- inutile`.

