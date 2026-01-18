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

#
