
# Homework JavaScript Avanzado I

## Scope & Hoisting

Determiná que será impreso en la consola, sin ejecutar el código.
4
> Investiga cuál es la diferencia entre declarar una variable con `var` y directamente asignarle un valor.

```javascript
x = 1; // Asignamos una variable directa combirtiendola en una variable global.
var a = 5; // Declaramos una variable a con numero 5.
var b = 10; // Declaramos una variable b con numero 10.
var c = function(a, b, c) {
  var x = 10; // declaramos una variable x con numero 10.
  console.log(x); // devuelve 10
  console.log(a); // devuelve 8
  var f = function(a, b, c) {
    b = a; // se reasigno la variable a numero 8.
    console.log(b); // retorna 8.
    b = c; // se reasigno la variable a 10.
    var x = 5; // se declaro una variable x con el numero 5.
  }
  f(a,b,c);
  console.log(b); // retorna el numero 9.
}
c(8,9,10);
console.log(b); // retorna el numero 10. BUSCA EN LA REASIGNACION QUE SE LE HIZO A (b = c) DENTRO DE LA FUNCION.
console.log(x); // retorna el numero 1. YA QUE BUSCA EN EL GLOBAL DEL CODIGO.
```

```javascript
console.log(bar); // Se rompe porque aun no a sido asignado nada a "bar".
console.log(baz); // Null porque al no asignar nada al console.log de "bar" no ejecuta.
foo();
function foo() { console.log('Hola!'); }
var bar = 1;
baz = 2;
```

```javascript
var instructor = "Tony"; // se asigna una variable intructor con el string "Tony".
if(true) {
    var instructor = "Franco"; // La variable instructor se modifica con otro strin cuyo nombre es "Franco".
}
console.log(instructor); // el console.log devuelve o imprime el "Franco" ya que la variable instructor fue modificada con cuyo nombre dentro de la funcion.
```

```javascript
var instructor = "Tony"; // se asigna una variable con un estring cuyo nombre es "Tony".
console.log(instructor); // se imprime la variable instructor el cual tiene por string "Tony".
(function() {
   if(true) {
      var instructor = "Franco"; // la variable intructor tiene una reasignacion con otro string cuyo nombre es "Franco".
      console.log(instructor); // aqui se imprime el console.log de instructor dentro de la funcion ya modificado el cual sera "Franco".
   }
})();
console.log(instructor); // este console.log imprime la variable global  "Tony" ya que no puede leer la variable dentro de la funcion inmediata invocada.
```

```javascript
var instructor = "Tony"; // se asigna una variable con el string por nombre "Tony".
let pm = "Franco"; // aqui se asigna una variable usando LET el cuyo string fue asignado como "Franco".
if (true) {
    var instructor = "The Flash"; // se modifica la variable instructor por otro string cuyo nombre se la "The Flash".
    let pm = "Reverse Flash"; // se modifica la variable LET de afuera de la fiuncion (OJO PERO ESTE LET SOLO FUNCIONA Y TRABAJA PARA ESTA FUNCION) cuyo string se le asigno como nombre "Reverse Flash".
    console.log(instructor); // el console.log imprime la variable "The Flash" hya que dicha fue modificada.
    console.log(pm); // el console.log imprime la variable LET "Reverse Flash" ya que esta variable LET solo imprime la variable que funciona dentro de esta funcion.
}
console.log(instructor); // el console.log imprime una variable intructor que fue modificada  con el string cuyo nombre fue asignado "The Flash".
console.log(pm); // el console.log imprime el LET asignado fuera de la funcion IF ya que cuyo LET solo funciona dentro de esa funcion asi imprimiendo el LET global que fue asigando por el string "Franco".
```
### Coerción de Datos

¿Cuál crees que será el resultado de la ejecución de estas operaciones?:

```javascript
6 / "3" // Aqui se ejecuta una division y con resultado de 0 ya que en JAVASCRIP no existe la division entre un STRING Y UN NUMERO.
"2" * "3" // se ejecuta una multiplicacion con resultado (6) que JAVASCRIP toma esos string y los convierte en numeros ya que no existe la multiplicacion de STRING.
4 + 5 + "px" // aqui se ejecuta primero una suma y luego se concatena el resultado de la suma con el STRING "px" dando como resultado ("9px")
"$" + 4 + 5 // aqui se concatenan los numeros con el STRING $ ya que al comenzar la operacion es un STRING y no hay suma entre un STRING y un numero, pero si se concatenan dando como resultado ("$45")
"4" - 2 // aqui se hace la resta dando resultado de (2) ya que no es posible hacer una operacion de resta entre un STRING y un numero.
"4px" - 2 // aqui da como resultado NaN ya que al no existir las operaciones de resta entre un string y un numero no existe, el STRING aparte de tener un numero anexa letras, asi haciendo que JAVASCRIP no pueda convertir el string en numero y realizar la operacion.
7 / 0 // esta operacion da como resultado infinito ya que la operacion imprime un resultado de numeros muy extensos.
{}[0] // aqui se ejecuta la los corchetes con el 0 ya que JAVASCRIP no toma encuenta las llaves ya que estan vacias y solo lee lo que esta dentro de los corchetes.
parseInt("09") // al ejecutar el parseInt es un metodo el cual JAVASCRIP solo toma en cuenta los numero enteros ya cuyo otros numeros los resta de la impresion dando como resultado ("9").
5 && 2 // JAVASCRIP aqui lee la LOGICA AND y imprime como resultado el (2) el ultimo elemento.
2 && 5 // JAVASCRIP aqui lee la LOGICA AND y imprime como resultado el (5) el ultimo elemento.
5 || 0 // JAVASCRIP aqui lee la LOGICA OR y imprime como resultado el (5), a diferencia de AND OR toma el numero TRUE en este caso 5.
0 || 5 // JAVASCRIP aqui lee la LOGICA OR y imprime como resultado el (5), a diferencia de AND OR toma el numero TRUE en este caso 5.
[3]+[3]-[10] // aqui JAVASCRIP lee una conquetanacion entre ([3]+[3]) ya que al estar dentro de corchetes se concatenan, luego JAVASCRIP lee una operacion de resta ya que a pesar de estar en corchetes no existe la operacion resta en JAVASCRIP asi dando como resultado (23).
3>2>1 // aqui JAVASCFRIP da como resultado FALSE ya que TRUE no es mayor que 1 la operacion se lee de esta manera (3 ES MAYOR QUE 2 = TRUE, AHORA TRUE ES MAYOR QUE 1 FALSE YA QUE TURE ES 1 Y NO ES MAYOR QUE 1).
[] == ![] // aqui se esta usando  un operador de igualdad pero NO ESTRICTA == "ESTO QUIERE DECIR QUE JAVASCRIP VERIFICA UNA IGUALDAD ASI IGNORANDO EL SIGNO DE EXCLAMACION DANDO COMO RESULTADO TRUE". 
```

> Si te quedó alguna duda repasá con [este artículo](http://javascript.info/tutorial/object-conversion).


### Hoisting

¿Cuál es el output o salida en consola luego de ejecutar este código? Explicar por qué:

```javascript
function test() {
   console.log(a); // devuelve UNDIFINED ya que JAVASCRIP por detras te sube la variable pero no esta definida.
   console.log(foo()); // te devuelve un (2) ya que la funcion (foo) te devuelve el numero (2).

   var a = 1;
   function foo() {
      return 2;
   }
}

test();
```

Y el de este código? :

```javascript
var snack = 'Meow Mix'; // asignacion de una variable

function getFood(food) {
    if (food) {
        var snack = 'Friskies';
        return snack; // no retorna nada ya que no entra la funcion ya que al llamarla es falso
    }
    return snack; // retorna UNDEFINED ya que JAVASCRIP me sube la variable indefinida y me la retorna.
}

getFood(false);
```


### This

¿Cuál es el output o salida en consola luego de ejecutar esté código? Explicar por qué:

```javascript
var fullname = 'Juan Perez'; // variable definida.
var obj = {
   fullname: 'Natalia Nerea', // variable definida.
   prop: {
      fullname: 'Aurelio De Rosa', // variable definida.
      getFullname: function() {
         return this.fullname; // retorna "Aurelio De Rosa" ya que esta dentro de la funcion.
      }
   }
};

console.log(obj.prop.getFullname()); // retorna "Aurelio De Rosa" ya que el console.log imprime y busca la funcion que esta dentro de la funcion valga a redundancia.

var test = obj.prop.getFullname; // copiamos la funcion en la variable TEST.

console.log(test()); // aqui se invoca la funcion TEST devolviendo "Juan Perez" ya que esta afuera de la llave asi buscando el fullname fuera de la funcion, en la global, definiendo el fullname de afuera con global. SI NO EN TODO CASO DA UNDEFINED.
```

### Event loop

Considerando el siguiente código, ¿Cuál sería el orden en el que se muestra por consola? ¿Por qué?

```javascript
function printing() {
   console.log(1); // devuelve 1 (ESTE CONSOLE.LOG ENTRA PRIMERO).
   setTimeout(function() { console.log(2); }, 1000); // devuelve 4 (ESTE CONSOLE.LOG ENTRA DE ULTIMO ASI DANDOLE LUGAR AL 4).
   setTimeout(function() { console.log(3); }, 0); // devuelve 3 (ESTE CONSOLE.LOG ENTRA TERCERO).
   console.log(4); // devuelve 2 (ESTE CONSOLE.LOG ENTRA DE ULTIMO YA QUE SI TIME ES DE 5 SEGUNDOS).
}

printing();
```
