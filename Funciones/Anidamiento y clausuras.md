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
    
        







