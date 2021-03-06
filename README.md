# Curso de Preprocesadores Web

Veremos Pug - Preprocesador HTML 
en CSS: 
- Sass
- Less
- Stylus 

# PUG
## Sintaxis

los archivos son de extensión ".pug"
No es necesario uusar los contenedores de las etiquetas "<>" ni en la apertura ni en el cierre.
para invocar las etiquetas unicamente necesitamos saber el nombre: `h1, p, span` 
para colocar elementos dentro de contenedores (nesting) puede ser tabular o espaciado.

```HTML
div 
    span
```
generaría 

```HTML
<div> 
    <span>
    </span>
</div>
```
### Es necesario asegurarse de selecionar una forma de indentación, ya sea TAB o espaciado, es posible que Pug no reconozca si se usan los dos. 

Para los metatags: 

```HTML
head 
    meta(charset="UTF-8")
```
para las hojas de estilo
```HTML
head 
    link(rel="stylesheet", href="unicacion/archivo.css")
```
uns estructura básica se escribiría asi: 
```HTML
doctype html
    head
        meta(charset="UTF-8")
        link(rel="stylesheet", href="ubicacion/archivo.css")
    body 
        header
            h1 Platzi-Preprocesadores
            a.boton //así agregamos clases
        section.intro
            .intro__imagen (prepros como compilador de preprocesadores, entiende que esto es un DIV) 
                img(src="images/imagen.jpg")
            // cuando solo hay un elemento hijo tambien se puede escribir
            .intro__imagen: img(src="images/imagen.jpg")
            .intro__contenido
                h2 Titulo 2
                p lorem
                a.boton Leer más
```

## Variables
HTML no tiene variables de forma nativa, esa es una de las fortalezas de los preprocesadores. 

Se recomienda que las variables se coloquen antes de todo para evitar conflictos. 
se declaran: 
```HTML
-var titulo = "Bienvenido a GitHub"
```

Se invocan de la siguiente forma: 
(dentro de un documento de PUG y una estructura HTML)
```HTML
h2= titulo
```
El signo igual debe ir pegado a la etiqueta, otra forma de invocar es: 
```HTML 
h2 #{titulo}
```
y puede causar menos confusión. Con todo se pueden hacer arreglos o arrays. 
se declaran: 
```HTML 
-var menuList = ["Home","About","Read More"]
```
Se invocan: 
```HTML 
h2 #{menuList[0]}
```
en este caso el "0" corresponde a la primera posición en el array o arreglo. 

## Condicionales y Ciclos (loops)
Cómo se escriben los ciclos: 
```HTML 
-var menuList = ["Home","About","Read More"]

ul
    each menuOption in menuList //declarando en ciclo
    li=menuOption
```
Cómo se escriben los condicionales
```HTML 
-var nombre = "Carlos"

if nombre
    p.login hola#{nombre}
else
    a.login Login
```
## Mixin
Son una forma de reutilizar código
Si tuvieramos 
```HTML 
oferta.contenido
    .box
        .box__img: img(src="images/imagen.png")
        .box__description
            h3 #{menuList[2]}
            p Lorem
```
Usualmente copiamos y pegamos n veces, donde n es el valor de la cantidad de cajas que tengamos. 
Dado el caso todo lo vamos a usar en un mixin, siempre se ponen al inicio

se declaran de la siguiente forma:
```HTML 
mixin oferta
    oferta.contenido
        .box
            .box__img: img(src="images/imagen.png")
            .box__description
                h3 #{menuList[2]}
                p Lorem
```
se invocan de la siguiente forma
```HTML 
    +oferta
    +oferta
    +oferta
```
Se llama n cantidad de veces 
pero que pasa cuándo necesitamos que el contenido de cada oferta sea distinta
En ese caso el Mixin recibe parametros. 
```HTML 
mixin oferta (img, menuList, description)// El contenido de los parentesis son los parametros
    oferta.contenido
        .box
            .box__img: img(src="images/"+img)//la ruta debería ser siempre la misma
            .box__description
                h3=menuList
                p=description
```
Y a la hora de invocar en los parentesis agregamos los parametros que deseamos modificar: 

```HTML 
    +oferta('nombreimagen', menuList[1], 'Texto de la descripción' )
    +oferta()
    +oferta()
```

## Extend e Include 
usualmente se utiliazan para los contenidos que se van a repetir, por ejemplos los head y los footer reguarlemte siempre son iguales. 
Es una buena práctica crear un drectorio de componentes. Son componentes los reutilizables dentro de la platilla. 
creado el head por ejmplo se invoca: 

```HTML 
doctype html
html
    include ruta/nombreDeArchivo.pug
```
cuando estamos generando plantillas y todo el header lo volvemos un archivo de pug debemos en el contenedor de el head la siguiente line

```HTML 
    block contenidos //en el final del documento a incluir a la altura del header, el block puede tener clauiqe nombre
```
y en el documento en el que se invoca ya no se usa el include si no un extend 
```HTML 
    extend ruta/nombreDeArchivo.pug
    block contenidos
    resto de códigp
```
la diferencia entre include y extend es que include agrega código más no permite agregar más (muestra error) mientras que extend si usamos el "block" con el nombre respectivo (podemos tener varios block) nos permitirá agregar más condigo en el momento que es invocado. 
Se podría usar include en el caso anterior? si, pero ordena el código de forma no deseada.
Además idealmente las variables y los mixin deberían de estar en su propio archivo de tal forma que sea "modular"





