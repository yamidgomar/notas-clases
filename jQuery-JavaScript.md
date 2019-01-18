# Curso de jQuery a JavaScript
#
# Índice
#

## [Sección I - Introducción](#sec1)
### [02 - La historia de jQuery](#clase2)
### [03 - Presentación del proyecto](#clase3)

#


## [Sección II - De jQuery a JavaScript](#sec2)
### [04 - Variables y Funciones](#clase4)
### [05 - Promesas](#clase5)
### [06 - Tutorial de Ajax en jQeury y Javascript](#clase6)
### [07 - Funciones Asíncronas](#clase7)
### [08 - Selectores](#clase8)
### [09 - Creación de templates](#clase9)
### [10 - Creación de DOM](#clase10)
### [11 - Reutilizando Funciones](#clase11)
### [12 - Eventos](#clase12)
### [13 - Clases y estilos CSS](#clase13)
### [14 - Creación de elementos y asignación de atributos](#clase14)
### [15 - Formularios](#clase15)
### [16 - Desestructuración de objetos](#clase16)
### [17 - DataSet](#clase17)
### [18 - Encontrando elementos en la lista](#clase18)
### [19 - Animaciones](#clase19)
### [20 - Manejo de errores](#clase20)
### [21 - LocalStorage](#clase21)
### [22 - Obteniendo los datos almacenados](#clase22)
### [23 - Conclusiones del curso](#clase23)

#

<br>
<br>
<br>

# <a name="sec1">Sección I - Introducción </a>

<br>
<br>

## <a name="clase2"> 02 - La historia de jQuery </a>


jQuery es una librería de JavaScript.
Cada librería resuelve un problema específico.

Las ventajas de jQuery fueron:

+ Una única forma de acceder al DOM de manera omogenea;

    Anteriormente se accedía al DOM por medio de selectores. Pero en esta época de incompatibilidad de browser y de Internet Explorer las formas de embeber JavaScript en nuestro código era diferente para cada browser.
    jQuery unificaba esta forma.
  
        $.('selector')


+ Interactuar con datos del servidor

    jQuery implementa Ajax (XML-HTTP-Request) para interactuar con servidores. 
    También ayudó a trabajar con la incompatibilidad de los selectores.
    
        $.ajax()


+ Animaciones

    Hacer animaciones era algo muy complejo también por la incompatibilidad de browsers y css tampoco tenía todas las funcionalidades que hoy tiene.

        $.animate()


    Con el paso del tiempo y de la implementación de jQuery comenzaron a aparecer "plugins" para esta librería que todavía facilitaban más las cosas.    
    Pero esto trajo la complicación de que nuestro código se mezclaba a tal punto que no se entendía qué era jQuery y qué era JavaScript, y con esto, la dificultad de hacer modificaciones en el mismo.
    
    Luego de esto aparecieron librerías para problemas específicos como **BackBone.js** que se apollaba sobre **underscores.js** para la funcionalidad y sobre **jQuery** para otras cosas.
    Las tecnologías evolucionaron.
    Actualmente han aparecido otros frameworks y ecosistemas más robustos como _REACT, ANGULAR o VUE_.
    
    Pero al fin y al cabo todo este sistema y nuevas tecnologías se apoyan en JavaScript Vanilla o en puro JavaScript.
    
    **Ventajas de Aprende JavaScript**
    
    + Reutilizar conocimiento en otros lados de tu aplicación
    + Poder implementar soluciones sin depender de una librería
    + Estar más capacitado para las grandes empresas

<br>
<br>
<br>

## <a name="clase3"> 03 - Presentación del proyecto </a>

Presentación del proyecto 'Platzi Video'sobre el que vamos a trabajar durante el curso.

Vamos a hacer todo esto en Vanilla JS, y te esteremos dando consejos de cómo hacer estos ejercicios con Jquery.

<br>
<br>
<br>

# <a name="sec2"> Sección II - De jQuery a JavaScript </a>

<br>
<br>

## <a name="clase4"> 04 - Variables y Funciones </a>

Para traer datos de un servicio externo vamos a usar en combinación:

  + Promesas
  + ajax/fetch
  + funciones asíncronas
 
**Procesos Asíncronos**

  Un proceso asíncrono es una petición que hace javaScript al browser y este la devuelve una vez cumplida a la _cola de tareas_ que será ejecutada al final del EventLoop o del flujo de funciones síncronas dentro de nuestro código.
  Por ejemplo cargar la página mientras pido al browser que obtenga todos los usuarios y los devuelva una vez cargado el sitio y cuándo esté listo.


Pero antes de implementar una Promesa demos tener en claro dos cosas necesarias: Variables y Funciones.

**Variables**

Dentro de JavaScript tenemos tres formas de declarar una **variable** las cuales son:

  + _var_ - ECMAScript 5
  + _let_ - A partir de ECMAScript 6      - Para declarar variables que pueden ser modificadas
  + _const_ - A partir de ECMAScript 6    - Para declarar variables que no pueden ser modificadas
  
**Funciones**

Las funciones son piezas de código que puedes reutilizar y se declaran con la palabra function.

    function estaEsMiFuncion(string){
        console.log(string)
    }


<br>
<br>
<br>

## <a name="clase5"> 05 - Promesas </a>

“Una Promesa es un objeto que representa la terminación o el fracaso eventual de una operación asíncrona”, o dicho de forma más cotidiana, se va a mandar (a dónde?) una función para ver si falla o se ejecuta con éxito.

Para crear una promesa:

    new Promise()
    
La guardamos en una nueva variable:

    const getUser = new Promise()
   
Las _Promesas_ reciben un argumento; este argumento es una función:

    const getUser = new Promise(function(){ })

Esta función que va a recibir como parámetro, a su vez recibe dos parámetros que son dos objetos; resolve y reject que nos van a indicar si nuestra _Promesa_ funcionó y no. 
El primero (resolve) será el que nos informe del resultado positivo y viceversa.
A estos los podemos llamar de otra manera:

    const getUser = new Promise( function(todoBien, todoMal) { })

Si mi request a una cierta API o de cualquier otro tipo es exitoso, la función parámetro de nuestra promesa devolverá el primer parámetro, si no el segundo.
Para ver cómo se comporta forzaremos la respuesta de esta función:

    const getUser = new Promise(function(todoBien, todoMal) {
        todoBien()
    })

Y para invocar a la promesa invoco a la variable _getUser_ encadenada al método _.then()_ que también recibe una función como variable

    getUser.then(function(){
        console.log(`El resultado de tu promesa es positivo.`)
    })
    
Para simular un delay en la _Promesa_ vamos a usar un _setTimeout()_. _**setTimeout()**_ es un método de JS que ejecuta una función después de un tiempo establecido. Y justamente recibe 2 parámetros; una función y una cantidad de tiempo en milisegundos.

```javascript

    const getUser = new Promise(function(todoBien, todoMal) {
        setTimeout(function(){
           todoBien()
        }, 3000)
    })
    
    getUser.then(function(){
        console.log(`El resultado de tu promesa es positivo.`)
    })
    // 3 seg. después:  El resultado de tu promesa es positivo.
    
```

Si el resultado de la _Promesa_ por cualquier cosa da un error o no funciona, llamamos al método _.catch()_ para capturar ese estado y al igual que con _.then()_ pasando una función como parámetro podemos manejar este error:


```javascript

    const getUser = new Promise(function(todoBien, todoMal) {
        setTimeout(function(){
           todoMal()
        }, 3000)
    })

    getUser
		.then(function(){
     	   console.log(`El resultado de tu promesa es positivo.`)
    	})
		.catch(function(){
        	console.log(`El resultado de tu promesa es negativo.`)
    	})
    

```

También podemos enviar parámetros a través de _todoBien()_ y _todoMal()_:


```javascript

    const getUser = new Promise(function(todoBien, todoMal) {
        setTimeout(function(){
           todoMal(`El resultado de tu promesa es negativo.`)  // paso el texto como parámetro
        }, 3000)
    })

    getUser
		.then(function(){
     	   console.log(`El resultado de tu promesa es positivo.`)
    	})
		.catch(function(message){  // recibo con 'message' el parámetro
        	console.log(message)
    	})
    

```

Si quiero eniar varias _Promesas_ de forma paralela?
Para esto uso el método .all() de _Promise_ que va a recibir un _'objeto[]'_ con todas las _Promesas_ previamente declaradas:


```javascript

    const getUser = new Promise ( (todoBien, todoMal) => setTimeout( () => todoBien(`El resultado de tu promesa es positivo.`), 1000 ))
    const getUser1 = new Promise((todoBien, todoMal) => setTimeout(() => todoBien(`El resultado de tu promesa es positivo II.`), 2000))
    const getUser2 = new Promise( (todoBien, todoMal) => setTimeout( () => todoBien(`El resultado de tu promesa es positivo III.`), 3000 ) )

    Promise.all([
        getUser,
        getUser1,
        getUser2
    ])
        .then( message => console.log(message))
        .catch( message => console.log(message))

    //depués de 3sec: (3) ["El resultado de tu promesa es positivo.", "El resultado de tu promesa es positivo II.", "El resultado de tu promesa es positivo III."]

```

Si aunque sea 1 de los Promises da error saldrá por .catch() y ninguna de las promesas funcionará.

Otro método usual con _Promesas_ es .race(). Este dara resultados a partir de la promesa que primero se resuelva.

```javascript

    const getUser = new Promise ( (todoBien, todoMal) => setTimeout( () => todoBien(`El resultado de tu promesa es positivo.`), 1000 ))
    const getUser1 = new Promise((todoBien, todoMal) => setTimeout(() => todoBien(`El resultado de tu promesa es positivo II.`), 2000))
    const getUser2 = new Promise( (todoBien, todoMal) => setTimeout( () => todoMal(`El resultado de tu promesa es negativo.`), 3000 ) )

    Promise.race([
        getUser,
        getUser1,
        getUser2
    ])
        .then( message => console.log(message))
        .catch( message => console.log(message))

    // El resultado de tu promesa es positivo.


```


<br>
<br>
<br>

## <a name="clase6"> 06 - Tutorial de Ajax en jQuery y Javascript </a

 Una característica muy solicitada en cualquier sitio dinámico es solicitar datos a un servidor, denominado API.
 
 Para hacer esto tenemos dos opciones:
 
   + Ajax con jQuery
   + fetch con Vanilla JS
   
**Ajax jQuery**

Ajax recibe dos parámetros los cuales son la url de la API y un objeto donde pondrás la configuración que se usara para realizar la petición. En la configuración se añaden dos funciones para manejar cuando la petición se realizo correctamente y cuando falla.

  _Referencia: http://api.jquery.com/jquery.ajax/_

```javascript

	$.ajax('htpps://randomuser.me/api/', {
		method: 'GET',
		success: function (data){
			console.log(data)
		},
		error: function (error) {
			console.log(error)
		}
	})

```
<br>

**JavaScript**

JavaScript internamente cuenta con una función llamada _fetch_ que también realiza peticiones a una API. 
Al igual que Ajax necesita dos parámetros, una url y una configuración, pero si solo le mandas la url fetch usará una configuración por defecto donde el método HTTP será GET.
_fetch_ te regresa una promesa, esa promesa al resolverse te da los datos de respuesta y tiene un método llamado _json()_ que te regresa otra promesa con los datos en formato JSON.

```javascript

	fetch("url")
	  .then( response => return response.json() )
	  .then( user => console.log(user) ) // datos en formato JSON
	  .catch( error => console.log(error) )

```
<br>

Las promesas resuelven el problema del Callback Hell haciendo que una promesa pueda devolver otra promesa y en lugar de ser anidadas como los callback, estas promesas son encadenadas.


<br>
<br>
<br>

## <a name="clase7"> 07 - Funciones Asíncronas </a>

Una función asíncrona va a ser como una función normal, pero poniendo código asíncrono de forma que sea más fácil de leer de forma síncrona.

Para declarar una función asíncrona se usa la palabra reservada _**async**_. Luego se declara la función de forma normal.
Dentro de una función asíncrona se usa otra palabra reservada llamada _**await**_, lo que hará este comando es indicar que se debe esperar a que termine de ejecutarse ese fragmento de código antes de continuar.


```javascript

	async function load() {
		await 
	}
	
```

Puedo llamar la función de manera normal:

```javascript

	async function load() {
		await 
	}
	load()

```

O puedo hacer que se autoejecute envolviéndola entre paréntesis:


```javascript

	(async function load() {
		await 
	})()

```

Para comenzar a trabajar en el ejercicio del curso usaremos la API de https://yts.am/api.
Genero un _fetch_ con la URL que necesito y lo guardo en una constante bajo el comando _**await**_
El código allí se detiene hasta que la promesa es devuelta y continúa con el código. 
Llamamos entonces al método _json()_ para obtener el objeto Promise con la 'data'.

```javascript

	(async function load(){
		const result = await fetch('https://yts.am/api/v2/list_movies.json?genre=action')
		const data = await result.json()
		console.log(data)
	})()

```

Ahora quiero traer tres promesas que corresponden a tres géneros diferentes de películas:

```javascript

	(async function load(){
		
		async function getData(url) {
			const result = await fetch(url)
			const data = await result.json()
			return data
		}
		
		const URLroot = 'https://yts.am/api/v2/list_movies.json?genre='
		
		const actionList = await getData(`${URLroot}action`)
		const horrorList = await getData(`${URLroot}horror`)
		const animationList = await getData(`${URLroot}animation`)
		
		console.log(actionList, horrorList, animationList)
	})()

```

<br>
<br>
<br>

## <a name="clase8"> 08 - Selectores </a>



<br>
<br>
<br>

## <a name="clase9"> 09 - Creación de templates </a>




<br>
<br>
<br>

## <a name="clase10"> 10 - Creación de DOM </a>




<br>
<br>
<br>

## <a name="clase11"> 11 - Reutilizando Funciones </a>




<br>
<br>
<br>

## <a name="clase12"> 12 - Eventos </a>




<br>
<br>
<br>

## <a name="clase13"> 13 - Clases y estilos CSS </a>




<br>
<br>
<br>

## <a name="clase14"> 14 - Creación de elementos y asignación de atributos </a>




<br>
<br>
<br>

## <a name="clase15"> 15 - Formularios </a>




<br>
<br>
<br>

## <a name="clase16"> 16 - Desestructuración de objetos </a>




<br>
<br>
<br>

## <a name="clase17"> 17 - DataSet </a>




<br>
<br>
<br>

## <a name="clase18"> 18 - Encontrando elementos en la lista </a>





<br>
<br>
<br>

## <a name="clase19"> 19 - Animaciones </a>





<br>
<br>
<br>

## <a name="clase20"> 20 - Manejo de errores </a>




<br>
<br>
<br>

## <a name="clase21"> 21 - LocalStorage </a>


<br>
<br>
<br>

## <a name="clase22"> 22 - Obteniendo los datos almacenados </a>




<br>
<br>
<br>

## <a name="clase23"> 23 - Conclusiones del curso </a>