En la página de descargas, haz clic en el botón **"Download for Windows"**. Esto descargará un archivo ejecutable.

<div style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; max-width: 100%;">
    <iframe 
        src="https://www.youtube.com/embed/WcYTcttEf50" 
        style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;" 
        frameborder="0" 
        allowfullscreen>
    </iframe>
</div>


> [!Note] Importante
> Ver detenidamente el video para la correcta instalación

# **Comandos Básicos**

## Configuración Inicial de Git

Antes de comenzar a usar Git, es importante configurar tu información de usuario. Esto se hace una sola vez por máquina.
```
git config --global user.name "Tu Nombre"
git config --global user.email "tuemail@example.com"
```
Puedes verificar tu configuración actual con:
## Clonar un Repositorio de GitHub

Para trabajar en un proyecto existente, primero debes clonar el repositorio desde GitHub a tu máquina local.
```
git clone https://github.com/usuario/nombre-del-repositorio.git
```
Reemplaza `usuario` y `nombre-del-repositorio` con los detalles correspondientes.
### Crear una Rama (`branch`)

Las ramas permiten trabajar en diferentes características o correcciones sin afectar la rama principal (`main` o `master`).

- **Crear una nueva rama:**
```
git branch nombre-de-la-rama
```
   
- **Crear y cambiar a una nueva rama en un solo paso:**
```
git checkout -b nombre-de-la-rama
```
Ejemplo
```
git checkout -b feature/nueva-funcionalidad
```
### Cambiar de Rama

Para cambiar a una rama existente:
```
git checkout nombre-de-la-rama
```
Ejemplo
```
git checkout main
```
### Agregar Cambios (`git add .`)

Este comando añade todos los cambios en el directorio actual al área de _staging_, preparándolos para ser confirmados.
```
git add .
```
> **Explicación:**
> 
> - El `.` (punto) representa el directorio actual y todos sus subdirectorios. Puedes especificar archivos individuales si lo prefieres, por ejemplo: `git add archivo.js`.

### Confirmar Cambios (`commit`)

Después de agregar los cambios al área de _staging_, necesitas confirmarlos con un mensaje descriptivo.
```
git commit -m "Descripción de los cambios realizados"
```
Ejemplo:
```
git commit -m "Añade la funcionalidad de autenticación de usuarios"
```
### Enviar Cambios al Repositorio Remoto (`push`)

Este comando envía tus confirmaciones locales al repositorio remoto en GitHub.

```
git push origin nombre-de-la-rama
```

Ejemplo:
```
git push origin feature/nueva-funcionalidad
```

**Nota:** Si es la primera vez que haces push a una nueva rama, puedes usar:
```
git push -u origin nombre-de-la-rama
```
Esto establece la rama remota como la rama de seguimiento predeterminada para la rama local.

### Actualizar el Repositorio Local (`pull`)

Para obtener y fusionar los cambios del repositorio remoto a tu rama local:
```
git pull origin nombre-de-la-rama
```
Ejemplo:
```
git pull origin main
```
