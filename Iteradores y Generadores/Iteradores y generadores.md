# **[Iteradores y generadores](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Iterators_and_generators#iterators)** #
---
## **Iteradores** ##

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

El iterador mas comun en js es el Array iterador, que devuelve cada valor del array asociado a la secuencia.
Sin embargo, no necesariamente se debe iterar sobre un array, podemos tener secuencias infinitas, o hasta el maximo numero representado por un entero.

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
```

