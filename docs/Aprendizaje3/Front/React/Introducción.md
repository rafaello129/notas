

# Introducción a React
<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%;">
    <iframe 
        src="https://www.youtube.com/embed/6Jfk8ic3KVk" 
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;" 
        frameborder="0" 
        allowfullscreen>
    </iframe>
</div>

### ¿Qué es React? Ventajas de React

**React** es una biblioteca de JavaScript desarrollada por Facebook para construir interfaces de usuario. No es un framework completo como Angular o Vue, sino que se enfoca en la capa de vista de una aplicación.

**Ventajas de React:**

- **Componentes Reutilizables**: Facilita la creación de componentes modulares y reutilizables, lo que mejora la mantenibilidad y escalabilidad de las aplicaciones.
- **Virtual DOM**: Utiliza un DOM virtual para mejorar el rendimiento al minimizar las manipulaciones directas del DOM real.
- **Unidireccionalidad de Datos**: Promueve un flujo de datos unidireccional, lo que simplifica el seguimiento de cambios y el manejo del estado de la aplicación.
- **Gran Comunidad y Ecosistema**: Cuenta con una amplia comunidad y numerosas herramientas, librerías y recursos disponibles.

### Conceptos Básicos para React

Antes de sumergirnos en React, es importante entender algunos conceptos clave:

- **Componentes**: Bloques de construcción fundamentales en React. Pueden ser clases o funciones que retornan elementos de React.
- **JSX (JavaScript XML)**: Sintaxis que combina JavaScript con HTML, permitiendo escribir elementos de manera declarativa.
- **Estado (State)**: Información que cambia con el tiempo y afecta la renderización de los componentes.
- **Props (Propiedades)**: Parámetros que se pasan a los componentes para configurar su apariencia o comportamiento.
- **Eventos**: Mecanismo para manejar interacciones del usuario, como clics o entradas de texto.

### Descargar e Instalar Node.js

Para trabajar con React, necesitamos tener instalado **Node.js**, ya que nos proporciona `npm` (Node Package Manager) para gestionar dependencias y paquetes.

**Pasos para la instalación:**

1. **Descargar Node.js**:

   - Visita [nodejs.org](https://nodejs.org/) y descarga la versión LTS (Long Term Support) recomendada.

2. **Instalar Node.js**:

   - Sigue las instrucciones del instalador según tu sistema operativo.
   - Asegúrate de que la instalación incluye `npm`.

3. **Verificar la Instalación**:

   - Abre una terminal y ejecuta:

     ```bash
     node -v
     npm -v
     ```

   - Deberías ver las versiones instaladas de Node.js y npm.

### Documentación Oficial de React

Es fundamental familiarizarse con la [documentación oficial de React](https://reactjs.org/). Allí encontrarás guías, tutoriales y referencias completas sobre la API de React.

---

## Introducción a JSX

### ¿Qué es JSX?

**JSX** es una extensión de sintaxis para JavaScript que permite escribir código similar a HTML dentro de JavaScript. Aunque puede parecer que estamos escribiendo HTML, en realidad estamos escribiendo sintaxis de React que será transformada en llamadas a la API de React mediante un compilador como Babel.

**Ejemplo de JSX:**

```jsx
const elemento = <h1>¡Hola, Mundo!</h1>;
```

### Elementos en React

Un **elemento** en React es la unidad más pequeña de las aplicaciones React. Representa lo que se renderiza en la pantalla.

**Ejemplo:**

```jsx
const elemento = <div className="contenedor">Contenido</div>;
```

### Diferencias entre Elemento y Componente

- **Elemento**: Es un objeto simple que describe lo que se debe ver en pantalla. Es inmutable y representa un nodo del DOM.
- **Componente**: Es una función o clase que puede aceptar entradas (props) y retorna un elemento de React.

### Introducción a `react-dom` y el DOM

**`react-dom`** es un paquete que proporciona métodos específicos para el DOM que permiten que React interactúe con el DOM del navegador.

- **DOM (Document Object Model)**: Es una interfaz de programación que permite a los lenguajes manipular la estructura y estilo de los documentos HTML y XML.

**Renderizar un elemento en el DOM:**

```jsx
import React from 'react';
import ReactDOM from 'react-dom';

const elemento = <h1>¡Hola, React!</h1>;
ReactDOM.render(elemento, document.getElementById('root'));
```

### Elementos HTML que se Pueden Usar

En JSX, puedes utilizar cualquier elemento HTML estándar, como `<div>`, `<span>`, `<h1>`, etc. Además, puedes crear tus propios componentes.

### Cómo Reconocer Elementos y Componentes

- **Elementos HTML**: Se escriben en minúsculas (`<div>`, `<p>`, `<input>`).
- **Componentes de React**: Se escriben con la primera letra en mayúscula (`<MiComponente />`).

### Atributos en JSX

Los atributos en JSX se parecen mucho a los de HTML, pero hay algunas diferencias:

- **`class`** se reemplaza por **`className`**.
- **`for`** se reemplaza por **`htmlFor`**.

**Ejemplo:**

```jsx
const elemento = <button className="btn">Click aquí</button>;
```

### Estructura JSX con Elementos Anidados

Puedes anidar elementos dentro de otros para crear estructuras más complejas.

**Ejemplo:**

```jsx
const elemento = (
  <div>
    <h1>Título</h1>
    <p>Este es un párrafo dentro de un div.</p>
  </div>
);
```

### Cómo Renderizar Componentes y Elementos

Para renderizar un componente, simplemente lo utilizas como si fuera un elemento JSX.

**Ejemplo de componente funcional:**

```jsx
function Bienvenida(props) {
  return <h1>¡Hola, {props.nombre}!</h1>;
}

ReactDOM.render(<Bienvenida nombre="María" />, document.getElementById('root'));
```

### Etiquetas Auto-Cerradas (Self-Closing Tags)

Algunos elementos HTML, como `<img>` o `<input>`, son auto-cerrados. En JSX, debes cerrarlos explícitamente.

**Ejemplo:**

```jsx
const imagen = <img src="imagen.jpg" alt="Descripción" />;
```

### Insertar JavaScript en JSX

Puedes insertar expresiones JavaScript dentro de JSX utilizando llaves `{}`.

**Ejemplo:**

```jsx
const usuario = 'Carlos';
const elemento = <h1>¡Hola, {usuario}!</h1>;
```

También puedes utilizar funciones o cálculos:

```jsx
const elemento = <p>La suma de 2 + 2 es {2 + 2}</p>;
```

---

## Estructura Inicial del Proyecto

### Crear la Estructura Básica con `create-react-app`

Para comenzar un nuevo proyecto de React de manera sencilla, utilizamos **Create React App**, una herramienta oficial que configura todo el entorno de desarrollo.

**Pasos para crear un nuevo proyecto:**

1. **Instalar Create React App (opcional si usas npx):**

   ```bash
   npm install -g create-react-app
   ```

2. **Crear un nuevo proyecto:**

   ```bash
   npx create-react-app mi-aplicacion
   ```

3. **Ingresar al directorio del proyecto:**

   ```bash
   cd mi-aplicacion
   ```

4. **Iniciar el servidor de desarrollo:**

   ```bash
   npm start
   ```

   Esto abrirá la aplicación en `http://localhost:3000`.

### Estructura de Carpetas y Archivos

- **`src/`**: Contiene el código fuente de la aplicación.
  - **`index.js`**: Punto de entrada principal.
  - **`App.js`**: Componente principal de la aplicación.
- **`public/`**: Contiene archivos estáticos.
- **`package.json`**: Lista de dependencias y scripts.
- **`node_modules/`**: Módulos instalados (no modificar).

---

## Recursos Adicionales

- **Documentación Oficial de React**: [https://reactjs.org/docs/getting-started.html](https://reactjs.org/docs/getting-started.html)
- **Tutorial Interactivo de React**: [https://reactjs.org/tutorial/tutorial.html](https://reactjs.org/tutorial/tutorial.html)
- **Guía de Estilo de JSX**: [https://reactjs.org/docs/jsx-in-depth.html](https://reactjs.org/docs/jsx-in-depth.html)
- **Create React App**: [https://create-react-app.dev/](https://create-react-app.dev/)

---
