# Arrow Function, Spread Operator, Deconstruction

## The Arrow Function (JS only)

La primera es la función de flecha. Veamos algunos ejemplos para ver cómo funciona:

```javascript
//una función normal:
function plus(a,b){
  return a + b;
}
//o podemos escribirla así:
let plus = function(a,b){
  return a + b;
}
//now, wo can use arrow function write it:
let plus = (a,b) => a + b;
         ~~~~~~~~~~  ------arrow function

```

Como puede ver, su sintaxis es
```javascript
(parameters) => {statement} or expression

(param1, paramN) => expression
```


```

Si sólo existe un parámetro en el lado izquierdo de la flecha, se puede omitir el corchete. Si sólo existe una expresión en el lado derecho de la flecha, también se pueden omitir las llaves. El ejemplo siguiente muestra una función con el () y el {} omitidos.

```javascript
let add = x => x + 1;
```

Si el lado derecho de la flecha es una declaración compleja, debe utilizar llaves:

```javascript
let pushElement = (arr,el1,el2) => {
  arr.push(el1);
  arr.push(el2);
  return arr;
}
console.log( pushElement([1],2,3) );

//output:
[ 1, 2, 3 ]
```

Hasta ahora, nuestros ejemplos han utilizado la asignación de funciones. Sin embargo, una función flecha también puede utilizarse como parámetro de una llamada a una función. Cuando se utiliza como parámetro, la función de flecha no requiere un nombre:

```javascript
let str="abababab";
console.log( strin.replace(/a/g, x => x.toUpperCase()) );

//output:
AbAbAbAb
```

String.replace toma una expresión regular y una función. La función se invoca en cada subcadena que coincida con la expresión regular, y devuelve el reemplazo de la cadena que coincida. En este caso, la función arrow toma la cadena coincidente como parámetro x, y devuelve el valor de x en mayúsculas.

En el momento de aprender el arrayObject y sus métodos, hay muchas aplicaciones en la función flecha, que es la razón por la que primero aprendemos la función flecha. La función flecha tiene un uso más complejo y restricciones de uso, pero no necesitamos aprender a ser tan profundos, así que sólo aprendemos el contenido de lo anterior.

Sin embargo, si la función flecha no toma parámetros, o más de un parámetro, un nuevo conjunto de paréntesis debe encerrar todos los argumentos:

```javascript
(() => "foo")() // -> "foo"

((bow, arrow) => bow + arrow)('I took an arrow ', 'to the knee...') 
// -> "I took an arrow to the knee..."
```

Ejemplos de función flecha:

```javascript
// Función tradicional
function (a){
  return a + 100;
}

// Desglose de la función flecha

// 1. Elimina la palabra "function" y coloca la flecha entre el argumento y el corchete de apertura.
(a) => {
  return a + 100;
}

// 2. Quita los corchetes del cuerpo y la palabra "return" — el return está implícito.
(a) => a + 100;

// 3. Suprime los paréntesis de los argumentos
a => a + 100;
```

```javascript

// Función tradicional
function (a, b){
  return a + b + 100;
}

// Función flecha
(a, b) => a + b + 100;

// Función tradicional (sin argumentos)
let a = 4;
let b = 2;
function (){
  return a + b + 100;
}

// Función flecha (sin argumentos)
let a = 4;
let b = 2;
() => a + b + 100;
```

Del mismo modo, si el cuerpo requiere **líneas de procesamiento adicionales**, deberás volver a introducir los corchetes **Más el "return"*:

```javascript
// Función tradicional
function (a, b){
  let chuck = 42;
  return a + b + chuck;
}

// Función flecha
(a, b) => {
  let chuck = 42;
  return a + b + chuck;
}
```

Y finalmente, en las **funciones con nombre** tratamos las expresiones de flecha como variables

```javascript
// Función tradicional
function bob (a){
  return a + 100;
}

// Función flecha
let bob = a => a + 100;
```

## Spread Operator

ES6 proporciona un nuevo operador llamado spread operator que consiste en tres puntos (...). 
El spread operator permite extender los elementos de un objeto iterable como un array, un map o un set. Por ejemplo:
```javascript
const odd = [1,3,5]; 

const combined = [2,4,6, ...odd]; 

console.log(combined);
```

Output: 
```javascript
[ 2, 4, 6, 1, 3, 5 ]
```

En este ejemplo, los tres puntos (...) situados delante del array <span style="color:red">impar</span> son el spread operator. 
El spread operator(...) desempaqueta los elementos del array <span style="color:red">impar</span>.

Tenga en cuenta que ES6 también tiene los tres puntos (...) que es un <u>rest parameter</u> que recoge todos los argumentos restantes de una función en un array.

```javascript
function f(a, b, ...args) {
	console.log(args); 
} 
f(1, 2, 3, 4, 5);
```

Output:
```javascript
[ 3, 4, 5 ]
```

En este ejemplo, el parámetro resto (...) recoge los argumentos 3, 4 y 5 en un array <span style="color:red">args</span>. Así que los tres puntos (...) representan tanto el spread operator como el rest parameter.

Estas son las principales diferencias:

- El spread operator (...) desempaqueta los elementos de un objeto iterable.
- El rest parameter (...) empaqueta los elementos en un array.

Los rest parameter deben ser los últimos argumentos de una función. Sin embargo, el operador spread puede estar en cualquier lugar:

```javascript
const odd = [1,3,5]; 

const combined = [...odd, 2,4,6]; 

console.log(combined);
```

Output:
```javascript
[ 1, 3, 5, 2, 4, 6 ]
```

ó:

```javascript
const odd = [1,3,5];

const combined = [2,...odd, 4,6];

console.log(combined);
```

Output: 
```javascript
[ 2, 1, 3, 5, 4, 6 ]
```


Veamos algunos escenarios en los que se pueden utilizar los spread operators.

## JavaScript spread operator y método apply() 

La siguiente función <span style="color:red">compare()</span> compara dos números:

```javascript
function compare(a, b) {
    return a - b;
}
```

En ES5, para pasar un array de dos números a la función <span style="color:red">compare()</span>, se suele utilizar el método <span style="color:blue">apply()</span> de la siguiente manera:

```javascript
let result = compare.apply(null, [1, 2]);

console.log(resultado); // -1
```

Sin embargo, utilizando el spread operator, puedes pasar un array de dos números a la función <span style="color:red">compare()</span>:

```javascript
let result = compare(...[1, 2]);

console.log(resultado); // -1
```

El spread operator extiende los elementos del array para que <span style="color:red">a</span> sea 1 y <span style="color:red">b</span> sea 2 en este caso.

## Ejemplo de cómo utilizar el método push() de Array de mejor forma

A veces, una función puede aceptar un número indefinido de argumentos. Llenar los argumentos desde un array no es conveniente.

Por ejemplo, el método <span style="color:red">push()</span> de un objeto array permite añadir uno o más elementos a un array. Si quieres pasar un array al método <span style="color:red">push()</span>, tienes que utilizar el método <span style="color:red">apply()</span> de la siguiente manera
```javascript
let rivers = ['Nilo', 'Ganges', 'Yangte'];
let moreRivers = ['Danubio', 'Amazonas'];

[ ].push.apply(rivers, moreRivers);
console.log(rivers);
```

El siguiente ejemplo utiliza el operador spread para mejorar la legibilidad del código:
```css
rivers.push(...moreRivers);
```

Como puede ver, el uso del spread operator es mucho más limpio.

## Spread operator y manipulación de arrays en JavaScript

1) Construcción de array literal

El operador spread permite insertar otro array en el array inicializado cuando se construye un array utilizando la forma literal. Vea el siguiente ejemplo:

```javascript
let initialChars = ['A', 'B'];
let chars = [...initialChars, 'C', 'D'];
console.log(chars); // ["A", "B", "C", "D"]
```

2) Concatenar arrays

También puedes utilizar el operador de propagación para concatenar dos o más arrays:
```javascript
let numbers = [1, 2];
let moreNumbers = [3, 4];
let allNumbers = [...numbers, ...moreNumbers];
console.log(allNumbers); // [1, 2, 3, 4]
```

3) Copiar un array

Además, puedes copiar una instancia de un array utilizando el spread operator:

```javascript
let scores = [80, 70, 90]; 
let copiedScores = [...scores]; 
console.log(copiedScores); // [80, 70, 90]
```

Observa que el spread operator sólo copia el propio array en el nuevo, no los elementos. Esto significa que la copia es superficial, no profunda.

##### El operador de propagación de JavaScript y las cadenas
Considere el siguiente ejemplo:

```javascript
let chars = ['A', ...'BC', 'D'];
console.log(chars); // ["A", "B", "C", "D"]
```

En este ejemplo, hemos construido el array chars a partir de cadenas individuales. Cuando aplicamos el spread operator a la cadena 'BC', se extiende cada carácter individual de la cadena 'BC' en caracteres individuales.

## Destructuring

El destructuring es también un nuevo miembro de ES6.

Primero, veamos un ejemplo sencillo de destructuring:

```javascript
let [a,b]=[1,2]; //el método antiguo es let a=1,b=2;
console.log(a);
console.log(b);
```

Output:
```javascript
1
2
```

La desestructuración nos permite asignar variables en forma de sentencia. He aquí un ejemplo un poco más complicado:

```javascript
let [a,b] = [1,2]
/Intercambiar los valores de las dos variables

//Método clásico:
let c = a; //definir c para ayudarnos
a = b
b = c;

//método de deconstrucción:
let [a,b] = [1,2];
[b,a] = [a,b];
console.log(a);
console.log(b);

//salida:
2
1
```

Con el destructuring, no necesitamos una variable temporal que nos ayude a intercambiar los dos valores.

Puedes utilizar el spread operator para el destructuring de la siguiente manera

```javascript
var [a,...b] = [1,2,3,4,5];
console.log(a);
console.log(b);

//salida:
1
[ 2, 3, 4, 5 ]
```

Atención: el spread operator debe ser la última variable: [...a,b] = [1,2,3,4,5] no funciona.

<span style="color:red">a</span> se asignó al primer elemento del array, y <span style="color:red">b</span> se inicializó con los elementos restantes del array.

El parámetro rest debe ser el último argumento de la lista de argumentos de la definición de la función.

En el siguiente ejemplo, utilizamos un rest parameter para recoger todos los valores pasados a mul() después del primero en un array. Luego multiplicamos cada uno de ellos por el primer parámetro y devolvemos ese array:

```javascript
function mul(a,...b){
  for (var i=0;i<b.length;i++) b[i]*=a;
  return b;
}
console.log(mul(2,1,1,1));
console.log(mul(2,1,2,3,4));
```

Output:
```javascript
[2,2,2]
[2,4,6,8]
```

***

## Ejercicios Arrow Function

### [1] 
Define an arrow function `divideByTwo` which accepts a number and returns that number divided by 2.

```javascript
console.log(divideByTwo(4)); //2
console.log(divideByTwo(8)); //4
console.log(divideByTwo(12)); //6
console.log(divideByTwo(6)); //3
```

<details><summary>Respuesta - ¡Haz Click!</summary>

```javascript
const divideByTwo = number => number / 2;
```

</details>


### [2] Two arguments

Transform this function:

```js

function sum(num1, num2){

return num1 + num2

}

  

sum(40,2)

sum(42,0)

console.log("the answer to everything is", sum(42,0))

```

  

<details><summary>Respuesta - ¡Haz Click!</summary>

  

This is a possible answer:

  

```js

const sum = (num1, num2) => num1+num2

```

You need parenthesis around the arguments because there are more than one.

You don't need curly brackets or the `return` keyword because arrow functions give you an implicit return.

  

However, this is also okay:

```js

const sum = (num1, num2) => {return num1+num2}

```

  

You can also use `let` but in that case your variable could be redefined later (which may cause bugs).

</details>


### [3] One argument

Transform this function that tells you how long a string is:

```js

function stringLength(str){

console.log(`the length of "${str}" is:`, str.length)

}

  

let longestCityNameInTheWorld = "Taumatawhakatangihangakoauauotamateaturipukakapikimaungahoronukupokaiwhenuakitanatahu"

  

stringLength(longestCityNameInTheWorld)

```

  

<details><summary>Respuesta - ¡Haz Click!</summary>

  

This is a possible answer:

  

```js

const stringLength = str => console.log(`the length of "${str}" is:`, str.length)

```

  

Here you don't need parenthesis aroung the argument because it's just one (but you could have the parenthesis, no difference).

You don't need curly brackets because it's just one line.

</details>


### [4] One argument, pt.2

Let's change the previous function a bit to include a variable and a return statement:

  
```js

function stringLength(str){

let length = str.length

console.log(`the length of "${str}" is:`, length)

return str.length

}

  

stringLength("willynilly")

```

  

<details><summary>Respuesta - ¡Haz Click!</summary>

  

This is a possible answer:

  

```js

const stringLength = str => {

let length = str.length

console.log(`the length of "${str}" is:`, length)

return str.length

}

  

stringLength("willynilly")

```

  

As you see, here you need an explicit return statement and curly brackets because it is a multiline function body.

</details>


### [5] One argument

Transform this function that selects a random element from the array and concatenates it to your name:

```js

let alerts = ["Hey, you are awesome", "You are so wonderful", "What a marvel you are", "You're so lovely", "You're so sweet that I'd think you're a sweet potato -- and I LOOOOVE POTATOES"]

  

function showAlert(name){

alert(alerts[(Math.floor(Math.random()*alerts.length))] + `, ${name}!`)

}

  

showAlert("you ball of fluff")

```

  

<details><summary>Respuesta - ¡Haz Click!</summary>

  

This is a possible answer:

  

```js

const showAlert = (name) => alert(alerts[(Math.floor(Math.random()*alerts.length))] + `, ${name}!`)

```

  

or:

```js

const showAlert = (name) => {return alert(alerts[(Math.floor(Math.random()*alerts.length))] + `, ${name}!`)}

```

</details>


### [6] Nested functions

Transform this function that rotates elements in your browser + remember about transforming also the traditional function in the `.map`:

```js

function oneTwoThreeRotate(){

Array.prototype.slice.call(document.querySelectorAll('div,p,span,img,a,body')).map(function(tag){

tag.style['transform'] = 'rotate(' + (Math.floor(Math.random() * 3) - 1) + 'deg)';

})

}

  

oneTwoThreeRotate()

```

  
<details><summary>Respuesta - ¡Haz Click!</summary>

This is a possible answer:

  

```js

const oneTwoThreeRotate = () => {

Array.prototype.slice.call( document.querySelectorAll('div,p,span,img,a,body')).map(tag => tag.style['transform'] = 'rotate(' + (Math.floor(Math.random() * 3) - 1) + 'deg)'

)

}

  

oneTwoThreeRotate()

```

  

Here we need the curly brackets because we have a multiline method but we don't need a return statement because we are not returning anything.

</details>



## Destructuring exercises

### Exercise [1]

Rewrite the code below to use array destructuring instead of assigning each value to a variable.

```javascript

let item = ["Egg", 0.25, 12];

let name = item[0];

let price = item[1];

let quantity = item[2];

console.log(`Item: ${name}, Quantity: ${quantity}, Price: ${price}`);

```


### Exercise [2]

Rewrite the code below to assign each number to the right variable.

```javascript

let numbers = [3, 5, 4, 2, 6, 1];

let [one, two, three, four, five, six] = numbers;

console.log(`One: ${one}, Two: ${two}, Three: ${three}, Four: ${four}, Five: ${five}, Six: ${six}`);

```

<details><summary>Respuesta - ¡Haz Click!</summary>
This is a possible answer:

```javascript  
let numbers = [3, 5, 4, 2, 6, 1];

let [three, five, four, two, six, one] = numbers;

console.log(  
`One: ${one}, Two: ${two}, Three: ${three}, Four: ${four}, Five: ${five}, Six: ${six}`  
);  
console.log();
```
	
</details>


### Exercise 3

We have an object called 'user'.

Write the destructuring assignment that reads:

- 'name' property into the variable 'name'.

- 'years' property into the variable 'age'.

- 'isAdmin' property into the variable 'isAdmin' (false, if no such property)


```javascript
console.log("EXERCISE 3");

let user = { name: "John", years: 30 };

// your code to the left side:

let {} = user;

console.log(name); // John

console.log(age); // 30

console.log(isAdmin); // false


```

<details><summary>Respuesta - ¡Haz Click!</summary>
```javascript
let user = { name: 'John', years: 30 };

// your code to the left side:  
let { name, years: age, isAdmin = 'false' } = user;

console.log(name); // John  
console.log(age); // 30  
console.log(isAdmin); // false  
console.log();
```
</details>


### Exercise 4

Rewrite the code below to use array destructuring instead of assigning each value to a variable.

```javascript

let person = [12, "Chris", "Owen"];

let firstName = person[1];

let lastName = person[2];

let age = person[0];

console.log(`Person - Age: ${age}, Name: ${firstName} ${lastName}`);

```

<details><summary>Respuesta - ¡Haz Click!</summary>
```javascript
let person = [12, 'Chris', 'Owen'];

let [age, firstName, lastName] = person;  
console.log(`Person - Age: ${age}, Name: ${firstName} ${lastName}`);  
console.log();
```
</details>


### Exercise 5

Rewrite the code below to use array destructuring instead of assigning each value to a variable.

Make sure not to have unused variables.

Hint: https://untangled.io/in-depth-es6-destructuring-with-assembled-avengers

```javascript

let person = ["Chris", 12, "Owen"];

let firstName = person[0];

let lastName = person[2];

console.log(`Name: ${firstName} ${lastName}`);

```

<details><summary>Respuesta - ¡Haz Click!</summary>
```javascript
let person = ['Chris', 12, 'Owen'];

let [firstName, lastName] = person;

console.log(`Name: ${firstName} ${lastName}`);  
console.log();
```
</details>


### Exercise 6

Using Array Destructuring get the last name from the array.

Hint: https://untangled.io/in-depth-es6-destructuring-with-assembled-avengers

```javascript

const students = ['Christina', 'Jon', 'Alexandare'];

// Write your code here

const [] = students;

console.log(lastName);

```

<details><summary>Respuesta - ¡Haz Click!</summary>
```javascript
const [, , lastName] = students;

console.log(lastName);  
console.log();  
}
```
</details>


### Exercise 7

Using Array Destructuring get all of the names from this Nested Array

Hint: https://untangled.io/in-depth-es6-destructuring-with-assembled-avengers

```javascript
const moreStudents = [

'Chris',

['Ahmad', 'Antigoni'],

['Toby', 'Sam']

];
```

<details><summary>Respuesta - ¡Haz Click!</summary>
```javascript
const moreStudents = ['Chris', ['Ahmad', 'Antigoni'], ['Toby', 'Sam']];  
let [student1, [student2, student3], [student4, student5]] = moreStudents;  
// Write your code here  
const [] = moreStudents;

console.log(student1, student2, student3, student4, student5);  
console.log();
```
</details>
