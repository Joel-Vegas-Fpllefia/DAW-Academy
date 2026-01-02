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