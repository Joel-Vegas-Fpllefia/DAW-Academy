# Transiciones

Es cuando realizamos una animacion entre un estado A a un estado B
**Se disparan cuando realizamo una accion concreta**, ejemplo movel el raton encima de un elemento

## Ejemplo

### Sin Transiciones

Aqui el cambio lo realiza de forma Brusca

```css
body {
  background-color: #223;
}

.box {
  width: 300px;
  height: 300px;
  border: 4px solid white;
  background-color: indigo;
}

.box:hover {
  background-color: red;
}
```

## Campos Transition

Al campo Transition tiene las siguiente propiedades: - 1º Caracteristica que va a cambiar - 2º Tiempo que va a tardar - 3º Ritmo que va a seguir

```css
transition: background 1s linear;
```

## Ejemplo con Transicion

# Animaciones

Cuando realizamos animaciones Css lo que estamos haciendo es una animacion que va a un estado A a un estado B a un estado C ...

Cuando realizamos animaciones basicas lo que estamos haciendo son **transiciones**

El usuario no tiene que realizar una accion concreta, es mas potente que las transiciones

# :active

Es un disparador de transicion que se ejecutara cuando se mantiene pulsado sobre el elemento

```css
.box:active {
  background: red;
}
```
