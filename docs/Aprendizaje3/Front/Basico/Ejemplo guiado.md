
**Creación de una Página Web desde Cero**

En este ejercicio práctico, aplicaremos todos los conceptos aprendidos desde el inicio para crear una página web completa utilizando **HTML** y **CSS**. Este ejercicio cubrirá desde la estructura básica de una página web hasta el uso de estilos avanzados como fondos, gradientes y sombras.

## Objetivo

- **Crear una página web estática** que incluya todos los elementos básicos de HTML y CSS aprendidos.
- **Aplicar estilos** para mejorar la presentación y experiencia del usuario.
- **Familiarizarse con el flujo completo de desarrollo web** desde cero.

---
## Pasos del Ejercicio

### 1. Entendiendo la Web

Antes de empezar, recordemos que la web funciona mediante la interacción entre clientes y servidores a través del protocolo HTTP. Los navegadores web solicitan páginas y recursos al servidor, que responde enviando los archivos necesarios (HTML, CSS, JavaScript, imágenes, etc.).

### 2. Preparación del Entorno de Desarrollo

- **Crear una Carpeta de Proyecto**: Crea una carpeta en tu computadora llamada `mi_pagina_web`.
- **Abrir el Proyecto en el Editor de Código**: Abre la carpeta en Visual Studio Code o tu editor preferido.

### 3. Estructura Básica de HTML

Crea un archivo llamado `index.html` y añade la estructura básica de una página web:

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Mi Página Web</title>
</head>
<body>

</body>
</html>
```

### 4. Uso de Párrafos y Encabezados

Dentro del `<body>`, agrega contenido utilizando encabezados y párrafos:

```html
<body>
  <h1>Bienvenidos a Mi Página Web</h1>
  <p>Esta es una página de ejemplo creada para practicar HTML y CSS.</p>

  <h2>Sobre Mí</h2>
  <p>Soy un apasionado del desarrollo web en constante aprendizaje.</p>
</body>
```

### 5. Creación de Listas

Añade una lista para destacar tus habilidades o intereses:

```html
<h2>Mis Habilidades</h2>
<ul>
  <li>HTML5 y CSS3</li>
  <li>JavaScript</li>
  <li>Desarrollo Responsive</li>
</ul>
```

### 6. Añadiendo Enlaces

Incorpora enlaces internos y externos:

```html
<p>Visita mi perfil en <a href="https://github.com/tu_usuario" target="_blank">GitHub</a>.</p>
<p>Para más información, ve a mi <a href="contacto.html">página de contacto</a>.</p>
```

Crea un archivo `contacto.html` con una estructura básica:

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Contacto</title>
</head>
<body>
  <h1>Contacto</h1>
  <p>Puedes enviarme un mensaje a través del formulario.</p>
</body>
</html>
```

### 7. Insertando Imágenes y Rutas

Agrega una imagen a tu página principal:

```html
<h2>Mi Fotografía</h2>
<img src="imagenes/mi_foto.jpg" alt="Fotografía personal">
```

- Crea una carpeta llamada `imagenes` dentro de `mi_pagina_web`.
- Coloca una imagen llamada `mi_foto.jpg` dentro de la carpeta `imagenes`.

### 8. Creación de Formularios

En `contacto.html`, añade un formulario para que los visitantes puedan contactarte:

```html
<form action="#" method="post">
  <label for="nombre">Nombre:</label><br>
  <input type="text" id="nombre" name="nombre"><br><br>

  <label for="email">Correo Electrónico:</label><br>
  <input type="email" id="email" name="email"><br><br>

  <label for="mensaje">Mensaje:</label><br>
  <textarea id="mensaje" name="mensaje" rows="5" cols="30"></textarea><br><br>

  <input type="submit" value="Enviar">
</form>
```

### 9. Introducción de CSS

Crea una carpeta llamada `css` y dentro de ella un archivo `estilos.css`. Enlaza la hoja de estilo en tus archivos HTML:

```html
<head>
  <meta charset="UTF-8">
  <title>Mi Página Web</title>
  <link rel="stylesheet" href="css/estilos.css">
</head>
```

Haz esto en `index.html` y `contacto.html`.

### 10. Aplicación de Selectores y Propiedades Básicas

En `estilos.css`, comienza a estilizar tu página:

```css
/* Selector universal */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* Selector de etiqueta */
body {
  font-family: Arial, sans-serif;
  background-color: #f4f4f4;
  color: #333;
}

/* Selector de clase */
.contenedor {
  width: 80%;
  margin: 0 auto;
}

/* Selector de ID */
#principal {
  padding: 20px;
}
```

Aplica las clases e IDs en tu HTML:

```html
<body id="principal">
  <div class="contenedor">
    <!-- Contenido aquí -->
  </div>
</body>
```

### 11. Uso de Tipografías Externas

Utiliza Google Fonts para añadir una tipografía personalizada:

- En tu `<head>`, agrega:

```html
<link href="https://fonts.googleapis.com/css?family=Roboto&display=swap" rel="stylesheet">
```

- En `estilos.css`, aplica la fuente:

```css
body {
  font-family: 'Roboto', sans-serif;
}
```

### 12. Modelo de Caja y Estilos de Contenedor

Estiliza el contenedor principal:

```css
.contenedor {
  background-color: #fff;
  padding: 20px;
  margin-top: 20px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}
```

### 13. Aplicación de Bordes, Márgenes y Rellenos

Aplica estilos a tus elementos:

```css
h1, h2 {
  margin-bottom: 15px;
}

p {
  line-height: 1.6;
  margin-bottom: 15px;
}

ul {
  list-style-type: square;
  margin-left: 20px;
}

img {
  max-width: 100%;
  height: auto;
  border: 5px solid #ccc;
}
```

### 14. Colores y Unidades

Define colores y unidades para un diseño coherente:

```css
body {
  color: #555;
}

a {
  color: #ff7e5f;
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}

input, textarea {
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
}

input[type="submit"] {
  width: auto;
  background-color: #ff7e5f;
  color: #fff;
  border: none;
  cursor: pointer;
}

input[type="submit"]:hover {
  background-color: #feb47b;
}
```

### 15. Fondos, Gradientes y Sombras

Añade estilos avanzados para mejorar el aspecto visual:

```css
/* Fondo con gradiente */
body {
  background: linear-gradient(to right, #ff7e5f, #feb47b);
}

/* Sombra de texto */
h1 {
  text-shadow: 2px 2px 5px rgba(0, 0, 0, 0.2);
}

/* Sombra de caja */
.contenedor {
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

/* Bordes redondeados */
img {
  border-radius: 10px;
}

/* Sombras en botones */
input[type="submit"] {
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2);
}
```

---

**Recursos Adicionales:**

- [MDN Web Docs - HTML](https://developer.mozilla.org/es/docs/Web/HTML)
- [MDN Web Docs - CSS](https://developer.mozilla.org/es/docs/Web/CSS)
- [Google Fonts](https://fonts.google.com/)
- [CSS-Tricks](https://css-tricks.com/)