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
