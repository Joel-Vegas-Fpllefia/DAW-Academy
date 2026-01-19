# Iniciar Proyecto

```shell
npm create vite@latest .
```

# Recoger datos de un JSON

```js
const datos = require("./datos.json");
```

# Introducir JS en React dentro del HTML

```js
<>
  <select name="" id="">
    {fp.map((ciclo) => (
      <option>{ciclo}</option>
    ))}
  </select>
</>
```

# Enviar Props a un componente

1. En el componente indicaremos lo que recibiremos por parametro:

```js
function SelectorPromocion({ciclos_formativos,setFpEstado} = props)
```

2. En App Iniciaremos el Componente y lo importaremos y luego le indicaremos el nombre de los paremetros puestos en el componente y entre {} lo que le vamos a enviar.

```js
<SelectorPromocion
  ciclos_formativos={fp}
  setFpEstado={setFpEstado}
></SelectorPromocion>
```

# Introducir comentarios en el return

```js
{
  /*Mostramos el Select con todas los ciclos formativos en contrados en el JSON/DB */
}
```

# UseState

Es la herramienta fundamenta para que los componentes puedan recordar cosa. Sin el los componentes seran simples funciones que se olvidan de todo lo que pasó en cuanto terminan de ejecutarse.

1. Importar useState en el archivo

```js
import React, { useState } from "react";
```

2. Crear el useState

```js
const [estado, setEstado] = useState(valorInicial);
```

3. Mostrar los valores de los estados
   Dentro del formulario introducir el campo value e introducir el valor:

```js
const [name, setName] = useState("Joel");
<input
  type="text"
  name="email"
  value={name}
  id="email"
  placeholder="prueba@gmail.com"
  required
  className="px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 text-gray-900"
/>;
```

4.  Cambiar el valor de la variable mediante va cambiando
    añadir el campo **onChange** en el html

5.  Destructurar el Evento capturado del onChange
    Para destructurar lo realizaremos de la siguiente forma

```js
const { name, value } = event.target;
```

6. Almacenar el valor introducido por el usuario
   Utilizar el Set para utilizar como puntero entre los nuevo y lo antiguo(se concatena solo), el cuale el value probiene del evento.

```js
setName(value);
```

# Useffect

Se usa para que cuando cambie un estado y queramos ejecutar una funcion

# LocalStorage

## Añadir campo

```js
localStorage.setItem("usuario", nombre);
```

## Recoger valor

```js
localStorage.getItem("usuario");
```

## Comprobar valor

```js
const nombre = localStorage.getItem("usuario");
console.log(nombre);
```

# Hook

# Recoger datos de un formulario

# Arrow Function

```js
const onLogin = () => {
  // tu código aquí
};
```

# Almacenar datos en el Local Storage

```js
localStorage.setItem("username", nameState);
```

# Recoger Datos del Local Storage

```js
const nombre = localStorage.getItem("username");
```

# PROPS

Son funciones las cuales se declare en el componente padre y se envia como parametro al componente hijo.

```js
// Componente hijo
function Hijo({ onClick }) {
  return <button onClick={onClick}>Clic aquí</button>;
}

// Componente padre
function Padre() {
  const saludar = () => alert("Hola desde el padre!");

  return <Hijo onClick={saludar} />; // pasa la función al hijo
}
```

# Cuando haga click en un boton enviar a un componente

# Añadir un nuevo Usuario al LocalStorage

```js
setStudentsState([...students_state, nuevoAlumno]);
```

# AJAX en JS

Teoria Completa: https://github.com/carrebola/2425M6/blob/main/UF4/AJAX.md

HTTP:
**ENDPOINT**, peticiones a: [GET,POST,PUT,DELETE] devuelve un JSON.
La Respuesta tambien **contiene el estado**.

GET --> Lee
POST --> Envia
PUT --> Reemplazar

## Codigos

404. Peticion al servidor pero el endpoint(el endpoint no lo encuentra)/archivo no lo contiene
405. Error interno del servidor
406. No tienes permiso al servidor

## Fetch API

forma parte de los navegadores, nos permite realizar peticiones a los navegadores.
**fetch**,

### Ejemplo basico con .then/.catch/.finally

```js
// fetch (funcion que devuelve un objeto/promesa)
// Promesa variable/objeto donde obtenemos un valor pero no de manera inmediata(podemos ver los estado:pendiente(pending toda via no hay nada),(error),(resuelta))
fetch("https://pokeapi.co/api/v2/pokemon/1") // Endpoint
  // Disparador
  // response resultado de la peticion
  .then((response) => {
    if (!response.ok) throw new Error(`HTTP ${response.status}`);
    return response.json();
  })
  .then((data) => console.log("Pokémon:", data.name))
  // Except en python
  .catch((err) => console.error("Error:", err))
  .finally(() => console.log("Petición finalizada"));
```

## fetch

Por defecto siempre sera un GET

## Promesa

variable/objeto donde obtenemos un valor pero no de manera inmediata(podemos ver los estado:pendiente(pending toda via no hay nada),(error),(resuelta))

## .then

Funcion que se va a ejecutar cuando tenga la respuesta del fetch, se suele usar un arrow function

## response

tiene varias propiedades

## Catch

Funcion que se funciona cuando ha habido un error

## Finally

Se ejecuta cuando termine el proceso (Siempre se ejecuta)

# Objetos en Fetch

```js
fetch(endpoint, {
  // Indicamos el metodo que realizara
  method: "POST",
  // Enviar un objeto en forma de texto
  body: "objetoDatos",
});
```

# Estados de promise

- Pending: en curso
- fulfilled: completada con éxito.
- rejected: completada con error

# Ejemplo de creacio y encadenamiento

```js
const promesa = new Promise((resolve, reject) => {
  setTimeout(
    // Si el numero es mayor a 0.5 devolvera Listo sino Fallo
    () => (Math.random() > 0.5 ? resolve("¡Listo!") : reject("Falló")),
    500
  );
});

promesa
  // Si es mayor a 0.5 Listo ejecutara el then
  .then((valor) => console.log(valor))
  // Si es reject ejecutar el catch
  .catch((error) => console.error(error))
  .finally(() => console.log("Proceso terminado"));
```

# Promesa encadenada

un .then dentro de otro .then

```js
fetch("https://pokeapi.co/api/v2/pokemon/1").then(
  fetch("https://pokeapi.co/api/v2/pokemon/2").then(
    fetch("https://pokeapi.co/api/v2/pokemon/3")
  )
);
```

# Promise.all (en paralelo)

el then se ejuctar cuando las peticiones del array asociado y se ejecutaran todos a la vez

```js
async function loadParallel() {
  const start = Date.now();
  try {
    const promises = [];
    for (let i = 1; i <= 12; i++) {
      // No lo rellena con datos si no con promesas
      promises.push(
        fetch(`https://pokeapi.co/api/v2/pokemon/${i}`).then((r) => r.json())
      );
    }
    // Cuando tenga todas las promesas resultas (mientras se van guardando los datos en pokemon) que espere
    const pokemons = await Promise.all(promises);
    // Mostramos los resultados obtenidos
    pokemons.forEach((p) => console.log(p.name));
  } catch (err) {
    console.error(err);
  } finally {
    console.log(`Paralelo en ${(Date.now() - start) / 1000}s`);
  }
}
loadParallel();
```

# Async/await

Forma moderna de hacer las peticiones en cadena, ya que una depende de la otra (las peticiones).

Con el Async podemos llamar a funcion sin obtener respuesta y seguir realizando peticiones.

Await => espera a que termine para saltar a la siguiente
Es codigo bloqueante ya que espara a que se ejecute esa linea y cuando termine saltara a la otra

```js
async function loadSequential() {
  const start = Date.now();
  try {
    const p1 = await fetch("https://pokeapi.co/api/v2/pokemon/1").then((r) =>
      r.json()
    );
    console.log(p1.name);
    // ... hasta p12
    const p12 = await fetch("https://pokeapi.co/api/v2/pokemon/12").then((r) =>
      r.json()
    );
    console.log(p12.name);
  } catch (err) {
    console.error(err);
  } finally {
    console.log(`Secuencial en ${(Date.now() - start) / 1000}s`);
  }
}
loadSequential();
```

# Promise.race

Se usa para cuando tengo la informacion en 5 servidores diferente lo ejecuto y si la primera que llega es correcta es que esta todo bien.

# JSON.stringify

# UseEfect

Vacio cada vez que se rederiza
Cuando hay uno Una vez que se modifica
