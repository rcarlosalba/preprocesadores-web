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
-var titulos = ["Titulo1","Titulo2","Titulo3"]
```
Se invocan: 
```HTML 
h2 #{titulo[0]}
```
en este caso el "0" corresponde a la primera posición en el array o arreglo. 

## Condicionales y Ciclos (loops)
