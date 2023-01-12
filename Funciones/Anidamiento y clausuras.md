 # **Anidamiento y Closures** #
 ---
## **Anidamiento** ##
 ``` javascript
//Un simple anidamiento
function  outer(x)
{

    function inner(y)
        {
        }
    inner(x);
}
```
> "La funcion interna (_inner_) puede acceder a **todos** los argumentos y variables del ambito de la funcion externa (_outer_). **La funcion externa es la unica que puede acceder a la funcion interna** "

```js
function addSquares(x,y)
{
    function square(z)
    {
        return z*z;
    }
    //Aquí la funcion interna (square)no está accediendo a los argumentos de la externa, sinó que esta se los está pasando por parametro.
    return square(x)+square(y);
}

addSquares(5,3);//Mostrará 34
```
---
## **[Closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)** ##

> "Una **Clausura** (_closure_) se forma cuando de alguna manera se **_expone_** y 
**_disponibiliza_** a la funcion interna a cualquier ámbito"

``` js 
    function outside(x)
    {
        function inside(y)
        {
            return x+y; //(I)
        }

        return inside;//(II)
    }

```

* Notar en (I) que aquí **si** la funcion interna esta accediendo a los argumentos de la funcion externa sin que esta se los pase.

* Notar en (II) que aquí se esta **exponiendo y disponibilizando** a  la funcion interna a cualquier ámbito (**se forma la clausura**).

``` javascript
    const sumar5=outside(5); //(III)
    sumar5(3);//Mostrara 8;

    outside(5)(3);//Mostrará 8 (sintaxis válida)
    
```
* En (III) sumar5 es _inside_ con el valor de x en 5

* **Importante**: Las variables y argumentos de la funcion externa **le pueden sobrevivir** a su ciclo de vida ya que pueden ser utilizadas por la funcion interna, ahora disponibilizada a cualquier ámbito

---

## **Clasurua y no clausura** ##

**Aunque el resultado es el mismo**

* **Esto es un anidamiento no una clausura**
    ``` js
    function init() {
    var name = 'Mozilla'; 
    function displayName() {
        
        console.log(name);
    }
    displayName();
    }
    init();
    ```
    > "La _**inner function**_ es exclusiva de la _**outer function**_
        , solo ella la llama"

* **Esto si una clausura**

    ```js
    function makeFunc() {
    const name = 'Mozilla';
    function displayName() {
        console.log(name);
    }
    return displayName;
    }

    const myFunc = makeFunc();
    myFunc();
    ```
    > "La _**inner function**_ esta expuesta y disponible a cualquier ambito"    
---
## **Lexical Environment** ##

>   "El  _**Lexical environment**_ es el **estado circundante** de una funcion.
    El estado de sus parametros reales y sus variables."


Veamos la funcion de suma
```js
   function makeAdder(x)
    {
        function add(y)
        {
            return x+y; //(I)
        }

        return add;//(II)
    }
```
Podemos verla como una fabrica de funciones de suma.
Luego:

``` js

    const sumar5=makedAdder(5);
    const sumar2=makedAdder(2);
```

>Aunque la funcion creadora es la misma (makeAdder) cada clausura tiene su propio
Lexical environment, en el de sumar5 x=5 y en el de sumar2 x=2.


---   
        
## **Usos prácticos** ##

>"Las clausuras son utiles porque nos permiten vincular datos con la funcion que
opera con esos datos. Esto va en consonancia con la **POO**. En consecuencia: podemos usar closures si necesitamos un objeto que solo tenga un metodo"

### **Un ejemplo pavo:** ###

```js
function Dog(name)
{
    function ladrar()
    {
        console.log(name +" "+"dice:Guau Guau!");
    }

    return ladrar;
}

var perro=Dog("Quebracho");
perro();// console output--> Quebracho dice: Guau Guau!
```




___

## **Emulando métodos privados con clausuras** ##

> "Solo los miembros de la clase (no su familia) ni externos pueden acceder" **POO*


```js 
const counter = (function () {

  let privateCounter = 0;

  function changeBy(val)
  {
    privateCounter += val;
  }

  return {
    increment() {
      changeBy(1);
    },

    decrement() {
      changeBy(-1);
    },

    value() {
      return privateCounter;
    },
  };
})();

console.log(counter.value()); // 0.

counter.increment();
counter.increment();
console.log(counter.value()); // 2.

counter.decrement();
console.log(counter.value()); // 1.

```
**Notar que**:

*   Se devuelve un objeto con 3 metodos
*   Son estos metodos los que acceden a lo privado:atributo (privateCounter) y metodo (changeby())

*   Estas 3 funciones publicas son clausuras que **comparten** el mismo lexical environment
