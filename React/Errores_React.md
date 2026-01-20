Uncaught TypeError: Cannot read properties of undefined (reading 'preventDefault')
Codigo Incorrecto:

```js
const changeValueName = (Event) => {
  Event.preventDefault();
  const { name, value_name } = Event.target;
  setName(nameState + name);
};

<input
  type="text"
  name="email"
  value={name}
  id="email"
  placeholder="prueba@gmail.com"
  required
  className="px-3 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-blue-500 text-gray-900"
  onChange={changeValueName()}
/>;
```

### Por que esta pasando

Llamamos a la funcion manualmente sin pasarle el objeto del evento

## Solcion

Llamar a la funcion sin **()**

```js
onChange = { changeValueName };
```

NameState UNDEFINED
Codigo Incorrecto

```js
const [nameState, setName] = useState("");
const [passwd, setPasswd] = useState("");
/*Arrow Function */
const changeValueName = (Event) => {
  Event.preventDefault();
  const { name, value_name } = Event.target;
  setName(value_name);
};
```

En JavaScript, la desestructuración de objetos (destructuring) busca nombres de propiedades específicos. Como el objeto e.target (el input) tiene una propiedad llamada value y no value_name, la variable queda como undefined si no coinciden.

```js
const changeValueName = (e) => {
  e.preventDefault();
  const { name, value } = e.target;
  setName(value);
};
```

Se envia por defecto el formulario y se queda en bucle
Codigo erroneo:

```js
onClick={onLogin(nameState, passwd)}
```

Se que da en bucle debido a que como le estoy enviado parametro a un evento debe estar envuelto por una arrow function,debido a que si a un evento le envio parametro tiene prioridad de ejecucion y se ejecuta de forma inmediata

Codigo correcto

```js
onClick={() => onLogin(nameState, passwd)}
```

# No se volvia a cargar la pagina

Error:
Usaba una variable normal

Solucion:
necesitaba usar un useEstate

# No detectaba a cual habia cambiado

Codigo malo:

```js
function SelectorPromocion({ ciclos_formativos, setFpEstado } = props) {
  function changeState(event) {
    console.log(event.target);
  }
  return (
    <select name="" id="" onChange={changeState}>
      <option value="">Seleccione un Ciclo Formativo</option>
      {ciclos_formativos.map((ciclo) => (
        <option name={ciclo} id={ciclo} value={ciclo}>
          {ciclo}
        </option>
      ))}
    </select>
  );
}

export default SelectorPromocion;
```

Problema en el console log el nombre no mostraba nada

Solucion:

Debido a que no tenia puesto el **value** en el campo **option**, no sabia a cual habia cambiado

```js
<select onChange={changeState}>
  <option value="">Seleccione un Ciclo Formativo</option>
  {ciclos_formativos.map((ciclo) => (
    <option value={ciclo}>{ciclo}</option>
  ))}
</select>
```

# Uncaught TypeError: Assignment to constant variable.

Codigo error:

```js
students_state = students_state.filter(
  (student) => student.ciclo === fp_estado,
);
```

El problema es que estamos intentando asignar un nuevo valor a una constante

# Uncaught Error: Too many re-renders. React limits the number of renders to prevent an infinite loop.

Codigo error:

```js
if (fp_estado != "") {
  const filter_fp = students_state.filter(
    (student) => student.ciclo === fp_estado,
  );
  setStudentsState(filter_fp);
}
```

El problema es que cada vez que se renderiza la web entra en el if y dentro del if esta el setStudent lo cual proboca otro disparador(el cual rederinza la pagina de nuevo y vuelve a entrar en el if) y se produce un loop / bucle infinito.

Para ello deberemos usar el UseEfect

Solucion:
El problema que tenia yo es que el setStudent hace rederizar de nuevo y eso entra en un loop pero con el useEffect si no se cambio no va a volver a entra

# No filtraba correctamente

El problema era que solo podria filtrar por el nombre y debia ser tal cual el nombre, la solucion era añadir tanto **lowerCase** en el array como el input del usuario, esto nos sirve para que ambos tengan **el mismo formato**

## No podria filtrar por palabrar en el medio / contenia esa letra

No podia / saber como filtrar por si contenia esa letra o no al final la solucion era el filtre junto un **includes**

```js
alumno.apellidos.toLowerCase().includes(search_user_estate.toLowerCase());
```

# No filtra por ambos campos:

El problema venia debido a que intentaba reutilizar el state como si fuera una variable, lo que pretendia era primero filtrarlo por nombre y pensaba que se quedaba guardado con ese filtro y luego queria volver a usarla ya filtrada para filtrar el curso.

PROBLEMA:
**El useState solo guarda la ultima llamada entonces cuando filtrabamos por curso no teniamos almacenado al usuario**

# Llama a la funcion si darle al boton de enviar

Tengo puesto en el boton enviar el evento onClick para cuando clique envie los datos pero se llama igual sin darle al btn, aparte al enviar datos y no poner previamente () => lo que hacia era llamar de forma directa a la funcion

```js
<>
  <input
    type="text"
    placeholder="Introduce Usuario"
    required
    value={name_logging}
    onChange={updateName}
  />
  <input
    type="password"
    name=""
    id=""
    value={password_logging}
    onChange={updatePasswd}
    required
  />
  <button onClick={() => onLogin(name_logging, password_logging)}>
    Iniciar Session
  </button>
</>
```

El problema era que como no teniamos preventDefault no para de enviarse de forma automatica ya que se renderizaba cada vez que escribiamos una letra

Solucion:

```js
<>
  <input
    type="text"
    placeholder="Introduce Usuario"
    required
    value={name_logging}
    onChange={updateName}
  />
  <input
    type="password"
    name=""
    id=""
    value={password_logging}
    onChange={updatePasswd}
    required
  />
  <button onClick={callFunction}>Iniciar Session</button>
</>
```

# Error en el if dentro de map

```js
admin_users.map((user_admin) =>
       if(name_user === user_admin.nombre && passwd_user === user_admin.password){
         console.log("HOLA")
       })
```

No podemos usar un if sin envolverlo en {}

# Cuando refresca una vez estando los datos filtrados se eliminan

# El array esta vacion cuando lo envio al componente

Estoy almacenando los datos en una lista y cuando los envio al componente esta vacio
Codigo erroneo:

```js
import { useState } from "react";
import reactLogo from "./assets/react.svg";
import viteLogo from "/vite.svg";
import "./App.css";

import Pokemon from "./components/pokemon";

function App() {
  const [visibility_poke, SetVisibility] = useState(false);
  // Actividad 2.1
  // const [list_poke, SetListPoke] = useState([]);
  let pokemon_list = [];
  function callback_hell() {
    const start = Date.now();
    SetVisibility(true);
    fetch("https://pokeapi.co/api/v2/pokemon/1")
      .then((r) => r.json())
      .then((p1) => {
        pokemon_list.push(p1);
        console.log("1: ", p1.name);
        fetch("https://pokeapi.co/api/v2/pokemon/2")
          .then((r) => r.json())
          .then((p2) => {
            pokemon_list.push(p2);
            console.log("2: ", p2.name);
          });
      });
  }

  return (
    <>
      <div>
        <div onClick={callback_hell}>
          <p>Exercici 2.1</p>
          <p>Tiempo: </p>
        </div>
        <div>
          <p>Exercici 2.2</p>
          <p>Tiempo: </p>
        </div>
        <div>
          <p>Exercici 2.3</p>
          <p>Tiempo: </p>
        </div>
      </div>

      <div className="card">
        {visibility_poke && <Pokemon list_pokemon={pokemon_list}></Pokemon>}
      </div>
      <p className="read-the-docs">
        Click on the Vite and React logos to learn more
      </p>
    </>
  );
}

export default App;
```

El problema es que la variable se envia vacia ya que cuando estoy rederizando el Componente Pokemon se estan llamando las API y aun no le ha dado tiempo a guardar los datos y ya se ha enviado los datos.
Solucion:
Usar un useState y un useEffect para renderizar por primera vez vacio

# Uncaught ReferenceError: callback_hell is not defined

```js
useEffect(
  // Funcion para act 1
  function callback_hell() {
    let pokemon_list = [];
    const start = Date.now();
    SetVisibility(true);
    fetch("https://pokeapi.co/api/v2/pokemon/1")
      .then((r) => r.json())
      .then((p1) => {
        pokemon_list.push(p1);
        console.log("1: ", p1.name);
        fetch("https://pokeapi.co/api/v2/pokemon/2")
          .then((r) => r.json())
          .then((p2) => {
            pokemon_list.push(p2);
            console.log("2: ", p2.name);
            fetch("https://pokeapi.co/api/v2/pokemon/3")
              .then((r) => r.json())
              .then((p3) => {
                pokemon_list.push(p3);
                console.log("3: ", p3.name);
                fetch("https://pokeapi.co/api/v2/pokemon/4")
                  .then((r) => r.json())
                  .then((p4) => {
                    pokemon_list.push(p4);
                    console.log("4: ", p4.name);
                    fetch("https://pokeapi.co/api/v2/pokemon/5")
                      .then((r) => r.json())
                      .then((p5) => {
                        pokemon_list.push(p5);
                        console.log("5: ", p5.name);
                        fetch("https://pokeapi.co/api/v2/pokemon/6")
                          .then((r) => r.json())
                          .then((p6) => {
                            pokemon_list.push(p6);
                            console.log("6: ", p6.name);
                            fetch("https://pokeapi.co/api/v2/pokemon/7")
                              .then((r) => r.json())
                              .then((p7) => {
                                pokemon_list.push(p7);
                                console.log("7: ", p7.name);
                                fetch("https://pokeapi.co/api/v2/pokemon/8")
                                  .then((r) => r.json())
                                  .then((p8) => {
                                    pokemon_list.push(p8);
                                    console.log("8: ", p8.name);
                                    fetch("https://pokeapi.co/api/v2/pokemon/9")
                                      .then((r) => r.json())
                                      .then((p9) => {
                                        pokemon_list.push(p9);
                                        console.log("9: ", p9.name);
                                        fetch(
                                          "https://pokeapi.co/api/v2/pokemon/10",
                                        )
                                          .then((r) => r.json())
                                          .then((p10) => {
                                            pokemon_list.push(p10);
                                            console.log("10: ", p10.name);
                                            fetch(
                                              "https://pokeapi.co/api/v2/pokemon/11",
                                            )
                                              .then((r) => r.json())
                                              .then((p11) => {
                                                pokemon_list.push(p11);
                                                console.log("11: ", p11.name);
                                                fetch(
                                                  "https://pokeapi.co/api/v2/pokemon/12",
                                                )
                                                  .then((r) => r.json())
                                                  .then((p12) => {
                                                    pokemon_list.push(p12);
                                                    console.log(
                                                      "12: ",
                                                      p12.name,
                                                    );
                                                    SetListPoke(pokemon_list);
                                                  });
                                              });
                                          });
                                      });
                                  });
                              });
                          });
                      });
                  });
              });
          });
      });
  },
  [],
);
```

Dentro del useEffect no podemos crear varias funciones pero si la podemos llamar:

```js
import { useEffect, useState } from "react";
import reactLogo from "./assets/react.svg";
import viteLogo from "/vite.svg";
import "./App.css";

import Pokemon from "./components/pokemon";

function App() {
  const [visibility_poke, SetVisibility] = useState(false);
  // Actividad 2.1
  const [list_poke, SetListPoke] = useState([]);
  // Funcion para act 1
  function callback_hell() {
    let pokemon_list = [];
    const start = Date.now();
    SetVisibility(true);
    fetch("https://pokeapi.co/api/v2/pokemon/1")
      .then((r) => r.json())
      .then((p1) => {
        pokemon_list.push(p1);
        console.log("1: ", p1.name);
        fetch("https://pokeapi.co/api/v2/pokemon/2")
          .then((r) => r.json())
          .then((p2) => {
            pokemon_list.push(p2);
            console.log("2: ", p2.name);
            fetch("https://pokeapi.co/api/v2/pokemon/3")
              .then((r) => r.json())
              .then((p3) => {
                pokemon_list.push(p3);
                console.log("3: ", p3.name);
                fetch("https://pokeapi.co/api/v2/pokemon/4")
                  .then((r) => r.json())
                  .then((p4) => {
                    pokemon_list.push(p4);
                    console.log("4: ", p4.name);
                    fetch("https://pokeapi.co/api/v2/pokemon/5")
                      .then((r) => r.json())
                      .then((p5) => {
                        pokemon_list.push(p5);
                        console.log("5: ", p5.name);
                        fetch("https://pokeapi.co/api/v2/pokemon/6")
                          .then((r) => r.json())
                          .then((p6) => {
                            pokemon_list.push(p6);
                            console.log("6: ", p6.name);
                            fetch("https://pokeapi.co/api/v2/pokemon/7")
                              .then((r) => r.json())
                              .then((p7) => {
                                pokemon_list.push(p7);
                                console.log("7: ", p7.name);
                                fetch("https://pokeapi.co/api/v2/pokemon/8")
                                  .then((r) => r.json())
                                  .then((p8) => {
                                    pokemon_list.push(p8);
                                    console.log("8: ", p8.name);
                                    fetch("https://pokeapi.co/api/v2/pokemon/9")
                                      .then((r) => r.json())
                                      .then((p9) => {
                                        pokemon_list.push(p9);
                                        console.log("9: ", p9.name);
                                        fetch(
                                          "https://pokeapi.co/api/v2/pokemon/10",
                                        )
                                          .then((r) => r.json())
                                          .then((p10) => {
                                            pokemon_list.push(p10);
                                            console.log("10: ", p10.name);
                                            fetch(
                                              "https://pokeapi.co/api/v2/pokemon/11",
                                            )
                                              .then((r) => r.json())
                                              .then((p11) => {
                                                pokemon_list.push(p11);
                                                console.log("11: ", p11.name);
                                                fetch(
                                                  "https://pokeapi.co/api/v2/pokemon/12",
                                                )
                                                  .then((r) => r.json())
                                                  .then((p12) => {
                                                    pokemon_list.push(p12);
                                                    console.log(
                                                      "12: ",
                                                      p12.name,
                                                    );
                                                    SetListPoke(pokemon_list);
                                                  });
                                              });
                                          });
                                      });
                                  });
                              });
                          });
                      });
                  });
              });
          });
      });
  }
  useEffect(callback_hell, []);

  return (
    <>
      <div>
        <div onClick={callback_hell}>
          <p>Exercici 2.1</p>
          <p>Tiempo: </p>
        </div>
        <div>
          <p>Exercici 2.2</p>
          <p>Tiempo: </p>
        </div>
        <div>
          <p>Exercici 2.3</p>
          <p>Tiempo: </p>
        </div>
      </div>

      <div className="card">
        {visibility_poke && <Pokemon list_pokemon={list_poke}></Pokemon>}
      </div>
      <p className="read-the-docs">
        Click on the Vite and React logos to learn more
      </p>
    </>
  );
}

export default App;
```

# const pokemons = await Promise.all(promises)

pokemons ya es una lista
