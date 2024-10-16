
## Introducción

El desarrollo web es un campo dinámico y en constante evolución. Esta guía te introducirá a los conceptos fundamentales de la creación de páginas web utilizando **HTML** y **CSS**. Aprenderás cómo estructurar contenido, aplicar estilos y crear páginas web atractivas y funcionales.
## Entendiendo la Web

La **Web** es una colección de documentos y recursos interconectados que se acceden a través de Internet. Los elementos clave para entender cómo funciona son:

- **Clientes y Servidores**: Un cliente (como un navegador web) solicita recursos de un servidor, que responde enviando los datos solicitados.
- **Protocolos**: El **HTTP** (HyperText Transfer Protocol) es el protocolo utilizado para la comunicación entre clientes y servidores.
- **URLs**: Las direcciones web que especifican la ubicación de los recursos en la web.

## Entendiendo HTML y CSS

- **HTML (HyperText Markup Language)**: Es el lenguaje estándar para crear y estructurar el contenido de una página web. Utiliza etiquetas para definir elementos como párrafos, encabezados, imágenes y enlaces.

- **CSS (Cascading Style Sheets)**: Es el lenguaje utilizado para describir la presentación de un documento HTML. Permite aplicar estilos como colores, fuentes, espaciados y disposición de elementos en la página.

## Editor de Código

Para escribir y editar código HTML y CSS, es recomendable utilizar un editor de código que facilite el desarrollo. Algunas opciones populares son:

- **Visual Studio Code**: Un editor gratuito y extensible con soporte para múltiples lenguajes.
- **Sublime Text**: Un editor ligero y rápido.
- **Atom**: Un editor de código abierto y personalizable.

---

## HTML BÁSICO

### Estructura de una Etiqueta

Las etiquetas HTML son la base de la estructura de una página web. Una etiqueta típica tiene la siguiente forma:

```html
<nombreDeEtiqueta atributos>
  Contenido
</nombreDeEtiqueta>
```

- **Etiqueta de apertura**: `<nombreDeEtiqueta>`
- **Contenido**: Puede ser texto, otras etiquetas o ambos.
- **Etiqueta de cierre**: `</nombreDeEtiqueta>`

Ejemplo:

```html
<p>Este es un párrafo.</p>
```

Algunas etiquetas son **auto-cerradas** y no requieren una etiqueta de cierre, como:

```html
<br> <!-- Salto de línea -->
<img src="imagen.jpg" alt="Descripción de la imagen">
```

### Estructura de una Página Web

Una página web básica tiene la siguiente estructura:

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Título de la Página</title>
</head>
<body>
  <!-- Contenido de la página -->
</body>
</html>
```

- `<!DOCTYPE html>`: Declara el tipo de documento como HTML5.
- `<html>`: Elemento raíz que contiene todo el contenido de la página.
- `<head>`: Contiene metadatos, como el título y enlaces a hojas de estilo.
- `<body>`: Contiene el contenido visible de la página.

### Párrafos y Encabezados

- **Encabezados**: Utiliza etiquetas `<h1>` a `<h6>` para definir títulos y subtítulos.

```html
<h1>Título Principal</h1>
<h2>Subtítulo</h2>
```

- **Párrafos**: Utiliza la etiqueta `<p>` para definir párrafos de texto.

```html
<p>Este es un párrafo de ejemplo.</p>
```

### Listas

Hay dos tipos principales de listas:

- **Listas Ordenadas**: Utiliza `<ol>` (ordered list) y `<li>` (list item).

```html
<ol>
  <li>Elemento 1</li>
  <li>Elemento 2</li>
</ol>
```

- **Listas No Ordenadas**: Utiliza `<ul>` (unordered list) y `<li>`.

```html
<ul>
  <li>Elemento A</li>
  <li>Elemento B</li>
</ul>
```

### Enlaces (Básico)

Los enlaces se crean con la etiqueta `<a>` y el atributo `href`.

```html
<a href="https://www.ejemplo.com">Visita Ejemplo</a>
```

- **Enlace interno**: Apunta a otra página dentro del mismo sitio.

```html
<a href="pagina2.html">Ir a Página 2</a>
```

- **Enlace externo**: Apunta a una página en otro sitio web.

### Imágenes y Rutas

Para insertar imágenes se utiliza la etiqueta `<img>`.

```html
<img src="ruta/imagen.jpg" alt="Descripción de la imagen">
```

- **Atributos importantes**:
  - `src`: Especifica la ruta de la imagen.
  - `alt`: Proporciona una descripción alternativa para la imagen.

**Rutas relativas y absolutas**:

- **Ruta relativa**: Se refiere a la ubicación del archivo en relación con la página actual.

```html
<img src="imagenes/foto.jpg" alt="Foto">
```

- **Ruta absoluta**: Especifica la ubicación completa, incluyendo el dominio.

```html
<img src="https://www.ejemplo.com/imagenes/foto.jpg" alt="Foto">
```

### Formularios

Los formularios permiten la entrada de datos por parte del usuario.

```html
<form action="procesar.php" method="post">
  <label for="nombre">Nombre:</label>
  <input type="text" id="nombre" name="nombre">
  
  <input type="submit" value="Enviar">
</form>
```

- **Elementos comunes**:
  - `<input>`: Campo de entrada. El atributo `type` define el tipo de dato (texto, contraseña, correo, etc.).
  - `<label>`: Etiqueta para el campo de entrada.
  - `<textarea>`: Campo de texto multilínea.
  - `<select>`: Menú desplegable.

---

## CSS BÁSICO

### Introducción a CSS

CSS se utiliza para estilizar elementos HTML. Hay tres formas de aplicar CSS:

1. **En línea**: Usando el atributo `style` en una etiqueta HTML.

```html
<p style="color: blue;">Texto azul</p>
```

2. **Interno**: Dentro de una etiqueta `<style>` en el `<head>`.

```html
<head>
  <style>
    p { color: blue; }
  </style>
</head>
```

3. **Externo**: En un archivo `.css` separado, vinculado con `<link>`.

```html
<head>
  <link rel="stylesheet" href="estilos.css">
</head>
```

### Selectores (Básico)

Los selectores determinan a qué elementos se aplican las reglas CSS.

- **Selector de etiqueta**:

```css
p {
  color: blue;
}
```

- **Selector de clase**: Se aplica a elementos con un atributo `class`.

HTML:

```html
<p class="importante">Texto importante</p>
```

CSS:

```css
.importante {
  font-weight: bold;
}
```

- **Selector de ID**: Se aplica a un elemento con un atributo `id`.

HTML:

```html
<h1 id="titulo-principal">Título</h1>
```

CSS:

```css
#titulo-principal {
  text-align: center;
}
```

### Propiedades de Texto y Fuente

- **Color de texto**:

```css
p {
  color: #333333;
}
```

- **Tipo de fuente**:

```css
p {
  font-family: Arial, sans-serif;
}
```

- **Tamaño de fuente**:

```css
p {
  font-size: 16px;
}
```

- **Estilo de fuente**:

```css
p {
  font-style: italic;
}
```

- **Peso de fuente**:

```css
p {
  font-weight: bold;
}
```

### Tipografías Externas

Puedes usar fuentes externas como Google Fonts.

**Paso 1**: Enlazar la fuente en el `<head>`.

```html
<head>
  <link href="https://fonts.googleapis.com/css?family=Roboto&display=swap" rel="stylesheet">
</head>
```

**Paso 2**: Aplicar la fuente en CSS.

```css
body {
  font-family: 'Roboto', sans-serif;
}
```

### Modelo de Caja (Box Model)

Cada elemento en HTML se considera como una caja que consta de:

- **Contenido**: El área donde se muestra el texto o imágenes.
- **Padding (Relleno)**: Espacio entre el contenido y el borde.
- **Border (Borde)**: El contorno del elemento.
- **Margin (Margen)**: Espacio fuera del borde que separa el elemento de otros.

![Modelo de Caja](https://developer.mozilla.org/es/docs/Learn/CSS/Building_blocks/The_box_model/box-model.png)

### Relleno y Margen (padding y margin)

- **Padding**: Añade espacio dentro del elemento.

```css
div {
  padding: 20px;
}
```

- **Margin**: Añade espacio fuera del elemento.

```css
div {
  margin: 10px;
}
```

### Bordes

Define el estilo, ancho y color del borde de un elemento.

```css
div {
  border: 2px solid #000000;
}
```

- **Estilos de borde**: `solid`, `dashed`, `dotted`, etc.

### Tamaño de Caja (box-sizing)

Controla cómo se calculan las dimensiones totales de un elemento.

- **`content-box`**: Valor predeterminado. El tamaño incluye solo el contenido.

- **`border-box`**: El tamaño incluye contenido, padding y borde.

```css
* {
  box-sizing: border-box;
}
```

### Colores

Puedes especificar colores en CSS utilizando:

- **Nombres de colores**:

```css
p {
  color: red;
}
```

- **Valores Hexadecimales**:

```css
p {
  color: #FF0000;
}
```

- **RGB/RGBA**:

```css
p {
  color: rgb(255, 0, 0);
}

div {
  background-color: rgba(0, 0, 0, 0.5); /* Transparencia */
}
```

### Unidades

Unidades comunes utilizadas en CSS:

- **Píxeles (`px`)**: Tamaño fijo.

```css
p {
  font-size: 16px;
}
```

- **Porcentajes (`%`)**: Relativo al elemento padre.

```css
div {
  width: 50%;
}
```

- **Em**: Relativo al tamaño de fuente del elemento padre.

```css
p {
  font-size: 1.5em;
}
```

- **Rem**: Relativo al tamaño de fuente raíz (`<html>`).

```css
p {
  font-size: 1rem;
}
```

---

**Recursos Adicionales:**

- [MDN Web Docs - Introducción a HTML](https://developer.mozilla.org/es/docs/Learn/Getting_started_with_the_web/HTML_basics)
- [MDN Web Docs - Introducción a CSS](https://developer.mozilla.org/es/docs/Learn/Getting_started_with_the_web/CSS_basics)
- [W3Schools - Tutoriales de HTML y CSS](https://www.w3schools.com/)

---

Para terminar, tenemos un ejemplo guiado usando los puntos ya vistos:
[Ejemplo guiado ](./Ejemplo%20guiado.md)