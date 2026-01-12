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
