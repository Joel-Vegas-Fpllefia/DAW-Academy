## Responsive
Tenemos estos 5 prefijos: 
(sin prefijo)	0px	Teléfonos pequeños (Móvil)
sm	640px	Teléfonos grandes / Tablets pequeñas
md	768px	Tablets (iPad)
lg	1024px	Laptops y Desktops
xl	1280px	Monitores grandes
2xl	1536px	Pantallas extra grandes

# Solo Mobil
si queremos que solo aparezca en el movil realizaremos lo siguiente: 
<h1 class="block md:hidden lg:hidden">J</h1> 
donde block indica que el elemento es como un bloque/visible

# Table y Desktop
<h1 class="hidden md:block lg:block">O</h1>

# Undidades de Medida
Todo se mide en md, Si nos dan **px dividirlo /4 y nos daran los md**

# Encabezados
En tailwind h1,h2,h3 no tienen ningun estilo por defecto
##  Escala de encabezados
### h1:
```css
text-4xl font-bold
```
### h2:
```css
text-3xl font-semibold
```
### h3:
```css
text-2xl font-medium
```

### h4: 
```css
text-xl font-medium
```
# Configurar Fuentes: 
```js
<script>
  tailwind.config = {
    theme: {
      extend: {
        fontFamily: {
          // 'serif' es el nombre de la clase que usarás, puedes ponerle 'titulo' si prefieres
          'source': ['"Source Serif 4"', 'sans-serif'],
        }
      }
    }
  }
</script>
```
**uso:**
```html
<h1 class="font-source text-4xl font-bold text-gray-900">
  Este título usa Source Serif
</h1>

<p class="font-source text-lg">
  Este texto también la utiliza.
</p>
```

# Flex elimina el tipo lista
si ha un elemento de una  lista (li) le indicamos que sea flex desaparecera el indicador ya que pasara a ser un texto 