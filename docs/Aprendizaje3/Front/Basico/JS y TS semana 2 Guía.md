# JavaScript y TypeScript 

### Configuración del Editor

- Instala extensiones útiles como:

  - **ESLint**: Para mantener un código limpio y consistente.
  - **Prettier**: Para formatear el código automáticamente.
  - **TypeScript**: Proporciona soporte para TypeScript en el editor.

### Primera Aplicación

Crea un directorio para tus proyectos y, dentro de él, un archivo `index.html` y un archivo `app.js`.

**index.html**:

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <title>Mi Primera Aplicación</title>
</head>
<body>
  <h1>¡Hola, Mundo!</h1>
  <script src="app.js"></script>
</body>
</html>
```

**app.js**:

```javascript
console.log('¡Hola desde app.js!');
```

Abre `index.html` en tu navegador y observa el mensaje en la consola.

### Referenciando Archivos

Es importante enlazar correctamente tus archivos JavaScript en el HTML. Utiliza la etiqueta `<script src="app.js"></script>` justo antes de cerrar el `</body>` para asegurarte de que el DOM se haya cargado antes de ejecutar el script.

---

## Tipos Básicos en JavaScript

### Variables

Las variables son contenedores para almacenar datos. En JavaScript, puedes declararlas utilizando `var`, `let` o `const`.

- **var**: Tiene un alcance de función y puede ser redeclarada.
- **let**: Tiene un alcance de bloque y puede ser reasignada, pero no redeclarada.
- **const**: Tiene un alcance de bloque y no puede ser reasignada ni redeclarada.

**Ejemplo**:

```javascript
let nombre = 'Juan';
const edad = 30;
var ciudad = 'Madrid';
```

### Reglas para Nombrar Variables

- Deben comenzar con una letra, `$` o `_`.
- No pueden comenzar con un número.
- Son **case-sensitive** (`nombre` y `Nombre` son diferentes).
- No pueden usar palabras reservadas.

### Tipos de Datos

JavaScript tiene tipos de datos **primitivos** y **objetos**.

#### Tipos Primitivos

- **string**: Cadenas de texto.

  ```javascript
  let mensaje = 'Hola, Mundo';
  ```

- **number**: Números (enteros y decimales).

  ```javascript
  let temperatura = 25.5;
  ```

- **boolean**: Verdadero o falso.

  ```javascript
  let esMayorDeEdad = true;
  ```

- **undefined**: Valor asignado automáticamente a variables no inicializadas.

- **null**: Representa ausencia de valor.

- **symbol**: Tipo único introducido en ES6.

#### Constantes

Utiliza `const` para declarar constantes, valores que no cambian durante la ejecución.

```javascript
const PI = 3.1416;
```

#### Tipado Dinámico

JavaScript es un lenguaje de tipado dinámico; una variable puede contener valores de diferentes tipos en distintos momentos.

```javascript
let valor = 42;
valor = 'Ahora soy una cadena';
```

#### Comentarios

- **Comentario de una línea**: `// Comentario`
- **Comentario de múltiples líneas**:

  ```javascript
  /*
    Este es un
    comentario de
    múltiples líneas
  */
  ```

### Objetos

Los objetos son colecciones de pares clave-valor.

**Ejemplo**:

```javascript
let persona = {
  nombre: 'Ana',
  edad: 28,
  ciudad: 'Barcelona',
};
```

Accedes a sus propiedades usando la notación de punto o corchetes:

```javascript
console.log(persona.nombre); // 'Ana'
console.log(persona['edad']); // 28
```

### Arrays

Los arrays son listas ordenadas de elementos.

**Ejemplo**:

```javascript
let colores = ['rojo', 'verde', 'azul'];
```

Accedes a sus elementos mediante índices:

```javascript
console.log(colores[0]); // 'rojo'
```

### Funciones

Las funciones son bloques de código reutilizables.

**Declaración de función**:

```javascript
function saludar(nombre) {
  return `Hola, ${nombre}`;
}
```

**Expresión de función**:

```javascript
const saludar = function (nombre) {
  return `Hola, ${nombre}`;
};
```

### Argumentos y Parámetros

- **Parámetros**: Variables definidas en la declaración de la función.
- **Argumentos**: Valores pasados a la función al invocarla.

**Ejemplo**:

```javascript
function sumar(a, b) {
  return a + b;
}

let resultado = sumar(5, 3); // a = 5, b = 3
```

---

## Operadores en JavaScript

### Declaraciones y Expresiones

- **Declaraciones**: Instrucciones que realizan una acción.

  ```javascript
  let x = 10;
  ```

- **Expresiones**: Fragmentos de código que producen un valor.

  ```javascript
  x + y;
  ```

### Operadores Aritméticos

- **Suma (+)**: `a + b`
- **Resta (-)**: `a - b`
- **Multiplicación (*)**: `a * b`
- **División (/)**: `a / b`
- **Módulo (%)**: `a % b` (resto de la división)
- **Incremento (++)**: `a++` o `++a`
- **Decremento (--):** `a--` o `--a`

### Operadores de Asignación

- **Asignación (=)**: `a = b`
- **Asignación con operación**:

  - `a += b` (equivale a `a = a + b`)
  - `a -= b`
  - `a *= b`
  - `a /= b`

### Operadores de Comparación

- **Igualdad estricta (=== ):** Compara valor y tipo.
- **Desigualdad estricta (!== )**
- **Mayor que (>)**, **Menor que (<)**
- **Mayor o igual que (>=)**, **Menor o igual que (<=)**

**Ejemplo**:

```javascript
let esIgual = (5 === '5'); // false
```

### Operadores Lógicos

- **AND (&&)**: Verdadero si ambos operandos son verdaderos.
- **OR (||)**: Verdadero si al menos uno es verdadero.
- **NOT (!)**: Invierte el valor lógico.

**Ejemplo**:

```javascript
let resultado = (a > 0) && (b > 0);
```

### Short Circuit

En operaciones lógicas, si el primer operando determina el resultado, el segundo no se evalúa.

- **AND (&&)**: Si el primer operando es `false`, el resultado es `false`.
- **OR (||)**: Si el primer operando es `true`, el resultado es `true`.

### Operadores Bitwise

Operan a nivel de bits. Algunos ejemplos son:

- **AND (&)**
- **OR (|)**
- **XOR (^)**
- **NOT (~)**
- **Shift Left (<<)**
- **Shift Right (>>)**

### Orden de Operaciones

JavaScript sigue un orden de precedencia en las operaciones, similar al matemático. Usa paréntesis `()` para controlar el orden.

### Operador Ternario

Sintaxis corta para una sentencia `if...else`.

**Sintaxis**:

```javascript
condición ? expresión_si_verdadero : expresión_si_falso;
```

**Ejemplo**:

```javascript
let esMayor = edad >= 18 ? 'Sí' : 'No';
```

---

## Control de Flujo

### Operador if

Permite ejecutar código basado en una condición.

**Ejemplo**:

```javascript
if (condición) {
  // Código a ejecutar si la condición es verdadera
}
```

### else

Proporciona una alternativa si la condición es falsa.

```javascript
if (condición) {
  // Si es verdadera
} else {
  // Si es falsa
}
```

### while

Ejecuta un bloque de código mientras una condición es verdadera.

```javascript
while (condición) {
  // Código a ejecutar
}
```

**Cuidado con los loops infinitos**: Asegúrate de que la condición cambiará en algún momento.

### do while

Similar a `while`, pero se ejecuta al menos una vez.

```javascript
do {
  // Código a ejecutar
} while (condición);
```

### for

Usado para iterar un número conocido de veces.

```javascript
for (inicialización; condición; actualización) {
  // Código a ejecutar
}
```

**Ejemplo**:

```javascript
for (let i = 0; i < 5; i++) {
  console.log(i);
}
```

### for...of

Itera sobre elementos iterables (arrays, strings).

```javascript
for (let elemento of iterable) {
  // Código a ejecutar
}
```

### for...in

Itera sobre las propiedades enumerables de un objeto.

```javascript
for (let propiedad in objeto) {
  // Código a ejecutar
}
```

### Continue y Break

- **continue**: Salta a la siguiente iteración.
- **break**: Sale del loop.

### switch

Selecciona entre múltiples opciones.

```javascript
switch (expresión) {
  case valor1:
    // Código si expresión === valor1
    break;
  case valor2:
    // Código si expresión === valor2
    break;
  default:
    // Código si ninguno coincide
}
```

---

## Introducción a TypeScript

### ¿Qué es TypeScript?

TypeScript es un superset de JavaScript que añade tipado estático y otras características avanzadas. Se compila a JavaScript puro, por lo que puede ejecutarse en cualquier entorno que soporte JavaScript.

TypeScript requiere un proceso de compilación para convertir el código TypeScript (`.ts`) a JavaScript (`.js`).

### Compilación en TypeScript

- **Instalar TypeScript** globalmente:

  ```bash
  npm install -g typescript
  ```

- **Compilar un archivo**:

  ```bash
  tsc archivo.ts
  ```

### Herramientas

- **tsc**: El compilador de TypeScript.
- **ts-node**: Permite ejecutar código TypeScript sin necesidad de compilarlo explícitamente.
- **Visual Studio Code**: Tiene excelente soporte para TypeScript.

### Inicio con TypeScript

- **Crear un proyecto**:

  ```bash
  mkdir mi-proyecto
  cd mi-proyecto
  npm init -y
  tsc --init
  ```

- **Configuración básica**: El comando `tsc --init` genera un archivo `tsconfig.json` para configurar el compilador.

---

## Tipos en TypeScript

### Tipos Básicos

- **string**
- **number**
- **boolean**
- **any**: Puede ser de cualquier tipo.
- **void**: Ausencia de tipo, generalmente en funciones que no retornan valor.
- **null** y **undefined**

**Ejemplo**:

```typescript
let nombre: string = 'Laura';
let edad: number = 25;
let esActivo: boolean = true;
```

### Tipado en Variables

TypeScript puede inferir el tipo de una variable a partir de su valor inicial.

```typescript
let mensaje = 'Hola'; // TypeScript infiere que es string
```

### Tipado en Funciones

- **Tipado de parámetros**:

  ```typescript
  function sumar(a: number, b: number): number {
    return a + b;
  }
  ```

- **Tipado de retorno**:

  ```typescript
  function saludar(nombre: string): string {
    return `Hola, ${nombre}`;
  }
  ```

### never y void

- **void**: Indica que una función no retorna un valor.

  ```typescript
  function logMensaje(mensaje: string): void {
    console.log(mensaje);
  }
  ```

- **never**: Indica que una función no finaliza su ejecución (lanza una excepción o entra en un loop infinito).

  ```typescript
  function error(mensaje: string): never {
    throw new Error(mensaje);
  }
  ```

### Objetos en TypeScript

Puedes definir el tipo de un objeto especificando sus propiedades y tipos.

```typescript
let persona: { nombre: string; edad: number } = {
  nombre: 'Carlos',
  edad: 40,
};
```

### Type Alias

Permite crear un alias para un tipo.

```typescript
type Punto = {
  x: number;
  y: number;
};

let coordenada: Punto = { x: 10, y: 20 };
```

### Propiedades Opcionales

Usa `?` para indicar que una propiedad es opcional.

```typescript
type Usuario = {
  nombre: string;
  email?: string; // Opcional
};
```

### Optional Chaining Operator

Permite acceder a propiedades anidadas sin causar errores si alguna es `undefined` o `null`.

```typescript
console.log(usuario?.email);
```

### Mutabilidad

- **Constantes**: Usa `const` para declarar variables que no cambian de referencia.
- **Inmutabilidad de objetos**: Puedes usar `Object.freeze()` para prevenir modificaciones.

### Template Union Types

Combina tipos literales y permite crear cadenas específicas.

```typescript
type Direccion = `${'Norte' | 'Sur'}-${'Este' | 'Oeste'}`;
let rumbo: Direccion = 'Norte-Este';
```

---

## Union Types e Intersection Types

### Union Types

Permite que una variable sea de uno u otro tipo.

```typescript
let resultado: string | number;
resultado = 'Aprobado';
resultado = 85;
```

### Intersection Types

Combina múltiples tipos en uno solo.

```typescript
type A = { x: number };
type B = { y: number };
type C = A & B;

let punto: C = { x: 10, y: 20 };
```

---

## Avanzando con TypeScript

### Type Indexing

Permite acceder a los tipos de las propiedades de un objeto.

```typescript
type Persona = { nombre: string; edad: number };
type Nombre = Persona['nombre']; // string
```

### Obtener Tipos de Valores y Funciones

- **typeof**: Obtiene el tipo de una variable o función.

  ```typescript
  let saludo = 'Hola';
  type TipoSaludo = typeof saludo; // string
  ```

### Arrays en TypeScript

Puedes tipar arrays indicando el tipo de sus elementos.

```typescript
let numeros: number[] = [1, 2, 3];
```

O usando `Array<T>`:

```typescript
let nombres: Array<string> = ['Ana', 'Luis', 'Pedro'];
```

### Matrices y Tuplas

- **Tuplas**: Arrays de longitud y tipos definidos.

  ```typescript
  let coordenadas: [number, number] = [10, 20];
  ```

---

**Recursos Adicionales**:

- [Documentación de JavaScript (MDN)](https://developer.mozilla.org/es/docs/Web/JavaScript)
- [Documentación de TypeScript](https://www.typescriptlang.org/docs/)
