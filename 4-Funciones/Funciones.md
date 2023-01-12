# Funciones en JavaScript #
---
## Secciones ##
* Sintaxis basica
* Funciones como variable
* Parametros
* Funciones flecha

---

### **Sintaxis básica** ###

```javascript

function miFuncion(parametro1,parametro2)
{
    //Esta es la implementacion de una funcion
    console.log("Hola Mundo");
    return;
}
```
### **Funciones como variable** ###
```js
//Funcion asignada a una variable miFuncion
const miFuncion=function (parametro1,parametro2)
{
    //Esta es la misma implementacion de una funcion
    console.log("Hola Mundo");
    return;  
}
```

### **Funcion Flecha** ###

```js
const myFuncion=(parametro1,parametro2)=>
{
    //Esta es la misma implementacion de una funcion con flecha
    console.log("Hola Mundo");
    return;  
}
```
### **Parametros por default** ###
```js
function miFuncion(parametro1=1,parametro2=0)
{
    //Esta es la implementacion de una funcion
    console.log("Hola Mundo");
    return;
}
```


