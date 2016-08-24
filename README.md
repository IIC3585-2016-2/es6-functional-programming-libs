# Librerías para programación funcional en javascript
---
Se van a revisar algunas de las principales librerías de programación funcional
para javascript, para cada libreria se mostrarán los mismo ejemplos, con el fin de resaltar las diferencias y similitudes en la sintaxis y alcance de las librerias.


## [Ramda.js: ](http://ramdajs.com/)
Al igual que la mayoría de las librerias revisadas, Ramda provee una [lista de funciones](http://ramdajs.com/0.22.1/docs/) que pueden ser utilizadas,a diferencia de otras librerías, Ramda está pensada en escribir codigo completamente funcional, manteniendo el foco en funciones libres de efectos secundarios que aseguren inmutabilidad.   
Las funciones provistas por Ramda están todas currificadas por defecto y se separan en las categorías: Math, Function, List, Logic, Object, Relation, String y Type.


#### 1. Instalación

```javascript
npm install ramda
```

```javascript
const R = require 'ramda'
```

#### 2. Ejemplos
Currying básico de una función, es importante notar que se puede elegir la posición del argumento que recibirá la función devuelta.
```javascript
let curriedSum = R.curry((a,b,c) => -a+b+c);
curriedSum(2,2)(4); // => 4
curriedSum(R.__,2,2)(4) // => 0
```

El orden de los argumentos sí importa, en el siguiente ejemplo, primero se le pasa el nombre de la propiedad a la función get, dado que es una función currificada, esto va a devolver una función que recibe el segundo argumento de la función original, por lo tanto, si se invierte el orden esto dejaría de funcionar.

```javascript
let objects = [{prop: 1}, {prop: 'uno'}, {prop: '1'}];
let get = R.curry((property, object) => object[property]);
objects.map(get('prop')); // => [ 1, 'uno', '1' ]
```


Una ventaja de Ramda es que sus funciones además de estar currificadas, siempre reciben como argumento primero el callback, lo que permite hacer algo como esto:

```javascript
const where = R.where({
  a: R.equals('foo'),
  b: R.complement(R.equals('bar')),
  x: R.gt(R.__, 10),
  y: R.lt(R.__, 20)
});

const arr = [ {a:  'foo', b: 'bars', x: 11, y:19},
            {a:  'foo', b: 'bar', x: 11, y:19},
            {a:  'foo', b: 'notabar', x: 15, y:0}];            
const filter = R.filter(where)
filter(arr) // => [ { a: 'foo', b: 'bars', x: 11, y: 19 },
            //     { a: 'foo', b: 'baras', x: 15, y: 0 } ]
```



## Referencias:
* http://ramdajs.com/0.22.1/docs/
* http://fr.umio.us/why-ramda/
