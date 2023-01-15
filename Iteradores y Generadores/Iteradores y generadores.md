# **[Iteradores y generadores](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_generators#iterators)** #
---
# **Iteradores** #

>"En **JAVA** y segun **Fontela (POO)**: Un iterador es un objeto que 'sabe moverse' a traves de los elementos de una collection (sin importar la estructura de la misma). Todo iterador debe implementar los siguientes métodos."

- Tomar el primer elemento
-   Tomar el elemento siguiente
-   Testear si se termino la colección


**Nosotros estamos trabajando en javascript asi que nos enfocaremos en su definicion.**

>   "En **_Javascript_** un **Iterador** es un **objeto** el cual define una **secuencia** y potencialmente retorna un valor al terminar. Un Iterador debe implementar el **Iterator Protocol** teniendo un método **_next_** que retorna un **objeto** con 2 atributos"

-   **Value**: El siguiente valor en la iteracion
-   **Done**:True si el ultimo elemento de la iteracion ha sido consumido.

**Si el value esta presente junto al Done, este sera el retorno del iterator.**


Una vez creado un objetor iterador puede ser iterado explicitamente con repetidas llamadas al metodo **next()**.
Se dice que iterar sobre el iterador **consume** el iterador, porque solo es posible hacerlo una vez.Despues de producido el valor de terminacion las llamadas a next() deberian continuar devolviendo {done:true}.

---
## **Iteration Protocols** ##

> "__Los protocolos de iteracion pueden ser implementados por cualquier objeto siguiendo algunas convenciones__"


__Existen 2 protocolos de iteracion: Iterable protocol y el Iterator protocol__ 

---
### __Iterable Protocol:__ ###

> "El protocolo iterable permite a los objetos de JavaScript definir o personalizar su comportamiento de iteracion ."

Algunos tipos de objetos de Javascript implementan el protocolo iterable por default con un comportamiento de iteracion determinado. Por ejemplo:
- Array
- Map
- Set 
- String
- Typed Array
- Segments
  
__Para ser iterable un objeto debe implementar el metodo @iterator (Devuelve un objeto iterator es el Constructor!), lo que significa que el objeto (o algun objeto superior en la cadena de prototipado) debe tener una propiedad(atributo) con la clave ___iterator___ la cual es accesible mediante la constante  Symbol.iterator__

Ejemplo en array:
 ```js
 let array=[1,2,3,4,5,6,7,8,9];
 let iterator=array[Symbol.iterator]();
 //El metodo retorna el iterator por default del array
```

> "Cuando se utiliza una instruccion __for each__ , __for..in__ en un arreglo __lo que se esta haciendo por detras es llamar al metodo iterator__ del objeto(o de su prototipo)

Cuando se llama a esta funcion de argumento 0 __se invoca como un metodo del objeto iterable__
por lo tanto, dentro de la funcion la palabra clave __this__ se puede usar para acceder a propiedades del objeto iterable.

---
### __Iterator Protocol:__ ###

> "El protocolo Iterador define una manera estandar para producir una __secuencia__ de valores (finita o infinita) y potencialmente un valor de retorno cuando todos los valores han sido generados"

Se espera que los métodos del protocolo iterador: next() result() y throw() (estos ultimos 2 opcionales) retornen un objeto que implemente la interfaz iteratorResult.


__Un objeto es un iterador cuando implementa un metodo _next()_ con la siguiente semantica:__

- __next()__ : Funcion que acepta uno o ningun argumento y retorna un __objeto__ conforme a la interfaz __IteratorResult__. Es decir que tenga las siguientes propiedades :

  - __value__:un valor de javascript devuelto por el iterador, puede ser omitido cuando done es true.
  - __done__: valor booleano, es falso si el iterador pudo producir el siguiente valor en la secuencia. Es TRUE si el iterador ha completado la secuencia (en este caso el value podria retornar el valor del iterador (cantidad de iteraciones)).





---
**Implementaremos un iterador utilizando una clausura**
``` js
function makeRangeIterator(start = 0, end = Infinity, step = 1) {
  let nextIndex = start;
  let iterationCount = 0;

  const rangeIterator = {
    next() {
      let result;
      if (nextIndex < end) {
        result = { value: nextIndex, done: false };
        nextIndex += step;
        iterationCount++;
        return result;
      }
      return { value: iterationCount, done: true };
    }
  };
  return rangeIterator;
}

const it = makeRangeIterator(1, 10, 2);

let result = it.next();
while (!result.done) {
 console.log(result.value); // 1 3 5 7 9
 result = it.next();
}

console.log("Iterated over sequence of size: ", result.value); // [5 numbers returned, that took interval in between: 0 to 10]

```
---
## __En resumen:__ ##
- 
  > "Un objeto es iterable si implementa el __iterator method__. Esto significa que el o su superior en la cadena de prototipado tiene definido la propiedad iterator. El __iterator method__ retorna un objeto __iterator__. Entonces __un objeto es iterable si tiene un metodo capaz de crear un iterador__".
  
  Luego

  > "Un objeto es un iterator si implementa el metodo __next()__ que retorna un objeto que implementa la __interface IteratorResult__ que debe tener las sig. propiedades:
    - done
    - value



---
## ASYNC Iteration protocols ##

There are another pair of protocols used for async iteration, named async iterator and async iterable protocols. They have very similar interfaces compared to the iterable and iterator protocols, __except that each return value from the calls to the iterator methods is wrapped in a promise.__


>__El protocolo iterable es el mismo, el protocolo iterator tambien solo que en vez de devolverse un objeto conforme a la interfaz IteratorResult se devuelve una promesa que se resuelve en un objeto conforme a la interfaz iterator result__

---

# __Generadores__ #

> "Los __objetos__ generadores son retornados por las __funciones generadoras__ e implementan tanto el protocolo iterable como el protocolo iterador"

## __Constructor__ ##

El constructor de objetos generator no esta disponible globalmente, la creacion de objetos generators debe realizarse mediante devoluciones de __funciones generadoras__