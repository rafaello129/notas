# NestJS: Creación de una API REST con MySQL, TypeORM y TypeScript



### ¿Qué es NestJS?

NestJS es un framework progresivo de Node.js para construir aplicaciones de servidor eficientes y escalables. Está construido con TypeScript y se inspira en Angular, lo que facilita la adopción para aquellos familiarizados con este framework frontend. NestJS utiliza una arquitectura modular, lo que promueve una separación clara de responsabilidades y facilita la mantenibilidad del código.

### ¿Por qué usar NestJS?

- **Arquitectura Modular:** Facilita la organización y reutilización de código.
- **Soporte para TypeScript:** Proporciona tipado estático, mejorando la calidad del código y la experiencia de desarrollo.
- **Integración con TypeORM:** Simplifica la interacción con bases de datos.
- **Inyección de Dependencias:** Facilita la gestión de dependencias y la creación de componentes desacoplados.
- **Comunidad Activa:** Amplio soporte y constante actualización de herramientas y librerías.


### ¿Qué es TypeORM?

TypeORM es un ORM (Object-Relational Mapping) que facilita la interacción entre aplicaciones TypeScript y bases de datos SQL. Proporciona una abstracción sobre las operaciones CRUD, permitiendo trabajar con entidades y repositorios en lugar de escribir consultas SQL manualmente.

### Características Principales

- **Soporte para múltiples bases de datos:** MySQL, PostgreSQL, SQLite, MariaDB, Microsoft SQL Server, Oracle, etc.
- **Decoradores para Definir Entidades:** Utiliza decoradores de TypeScript para definir modelos de datos.
- **Migraciones:** Facilita la gestión de cambios en el esquema de la base de datos.
- **Relaciones entre Entidades:** Soporta relaciones uno a uno, uno a muchos y muchos a muchos.
- **Query Builder:** Permite construir consultas complejas de manera programática.
- **Active Record y Data Mapper:** Soporta ambos patrones de diseño.

### Instalación y Configuración

Para integrar TypeORM con NestJS, es necesario instalar los paquetes correspondientes y configurar la conexión a la base de datos.

```bash
npm install --save @nestjs/typeorm typeorm mysql2

En el archivo `app.module.ts`, se configura el módulo de TypeORM:

```typescript
import { TypeOrmModule } from '@nestjs/typeorm';

@Module({
  imports: [
    TypeOrmModule.forRoot({
      type: 'mysql',
      host: 'localhost',
      port: 3306,
      username: 'tu_usuario',
      password: 'tu_contraseña',
      database: 'nombre_de_la_base_de_datos',
      entities: [__dirname + '/**/*.entity{.ts,.js}'],
      synchronize: true,
    }),
    // Otros módulos
  ],
})
export class AppModule {}
```


---

### ¿Qué es Nest.js CLI?

El CLI (Command Line Interface) de NestJS es una herramienta poderosa que simplifica la creación y gestión de proyectos NestJS. Permite generar módulos, controladores, servicios y otros componentes de manera automática, siguiendo las mejores prácticas del framework.

### Instalación del CLI

Para instalar el Nest.js CLI de manera global, ejecuta:

```bash
npm install -g @nestjs/cli
```

### Creación de un Nuevo Proyecto

Utiliza el siguiente comando para crear un nuevo proyecto NestJS:

```bash
nest new nombre-del-proyecto
```

Este comando genera la estructura básica del proyecto, instala las dependencias y configura el entorno de desarrollo.

### Comandos Básicos del CLI

- **Generar Módulo:**

  ```bash
  nest generate module nombre-modulo
  ```

- **Generar Controlador:**

  ```bash
  nest generate controller nombre-controlador
  ```

- **Generar Servicio:**

  ```bash
  nest generate service nombre-servicio
  ```

- **Generar Recurso:**

  ```bash
  nest generate resource nombre-recurso
  ```

  Este comando genera un módulo, controlador y servicio para un recurso específico, facilitando la creación de APIs RESTful.

---

### ¿Qué es Docker Compose?

Docker Compose es una herramienta para definir y gestionar aplicaciones multicontenedor de Docker. Permite definir los servicios, redes y volúmenes de la aplicación en un archivo `docker-compose.yml`, facilitando la orquestación y despliegue de entornos de desarrollo consistentes.

### Instalación de Docker y Docker Compose

1. **Instalar Docker Desktop:**
   - Descarga e instala Docker Desktop desde [Docker Hub](https://www.docker.com/products/docker-desktop).

2. **Verificar la Instalación:**

   ```bash
   docker --version
   docker-compose --version
   ```

### Configuración de Docker Compose para MySQL

Crea un archivo `docker-compose.yml` en la raíz de tu proyecto con la siguiente configuración:

```yaml
version: '3.8'

services:
  db:
    image: mysql:8.0
    restart: always
    environment:
      MYSQL_DATABASE: nombre_de_la_base_de_datos
      MYSQL_USER: tu_usuario
      MYSQL_PASSWORD: tu_contraseña
      MYSQL_ROOT_PASSWORD: tu_contraseña_root
    ports:
      - "3306:3306"
    volumes:
      - db_data:/var/lib/mysql

volumes:
  db_data:
```

### Uso de Docker Compose

1. **Iniciar los Servicios:**

   ```bash
   docker-compose up -d
   ```

   Este comando descarga la imagen de MySQL, crea y ejecuta el contenedor en segundo plano.

2. **Detener los Servicios:**

   ```bash
   docker-compose down
   ```

3. **Verificar los Contenedores en Ejecución:**

   ```bash
   docker ps
   ```

### Ventajas de Usar Docker Compose

- **Consistencia en Entornos:** Asegura que todos los desarrolladores trabajen con las mismas configuraciones.
- **Facilidad de Uso:** Simplifica el inicio y parada de servicios con comandos sencillos.
- **Escalabilidad:** Permite añadir más servicios fácilmente, como servidores de caché, APIs adicionales, etc.

---

## Visualizar Base de Datos

### Herramienta Recomendada: DBeaver

### Instalación de DBeaver

1. **Descargar DBeaver:**
   - Visita [https://dbeaver.io/download/](https://dbeaver.io/download/) y descarga la versión Community para Windows.

2. **Ejecutar el Instalador:**
   - Sigue las instrucciones del asistente de instalación.

3. **Configurar la Conexión a MySQL:**

   - **Abrir DBeaver:**
     - Inicia DBeaver desde el menú de inicio o el acceso directo.

   - **Crear una Nueva Conexión:**
     - Haz clic en el botón **"New Database Connection"**.

   - **Seleccionar MySQL:**
     - Elige **MySQL** de la lista de bases de datos y haz clic en **"Next"**.

   - **Ingresar los Detalles de Conexión:**
     - **Host:** `localhost`
     - **Port:** `3306`
     - **Database:** `nombre_de_la_base_de_datos`
     - **Username:** `tu_usuario`
     - **Password:** `tu_contraseña`

   - **Probar la Conexión:**
     - Haz clic en **"Test Connection"** para verificar que los detalles son correctos.

   - **Finalizar la Configuración:**
     - Si la prueba es exitosa, haz clic en **"Finish"**.

Puedes usar el que mas te guste 

---

## CLI Resource Cats

### Creación de Recursos con Nest.js CLI

Para estructurar la API de manera eficiente, Nest.js CLI ofrece comandos para generar recursos completos, incluyendo módulos, controladores y servicios.

### Generar un Recurso: Cats

Ejecuta el siguiente comando para generar un recurso llamado `cats`:

```bash
nest generate resource cats
```

### Estructura Generada

Este comando crea:

- **Módulo:** `cats.module.ts`
- **Controlador:** `cats.controller.ts`
- **Servicio:** `cats.service.ts`
- **DTOs:** Data Transfer Objects para manejar datos de entrada y salida.
- **Interfaces:** Definición de la estructura de los datos.

---

### Introducción a Class Validator

**Class Validator** es una biblioteca que permite realizar validaciones en las propiedades de las clases utilizando decoradores. Es especialmente útil para validar datos de entrada en APIs, asegurando que los datos cumplen con ciertos criterios antes de ser procesados.

### Instalación

Para instalar Class Validator y Class Transformer, ejecuta:

```bash
npm install --save class-validator class-transformer
```

### Uso en NestJS

1. **Crear DTOs con Validaciones:**

   Define DTOs (Data Transfer Objects) utilizando decoradores de validación para asegurar que los datos recibidos cumplen con los requisitos.

   ```typescript
   import { IsString, IsInt, Min, Max } from 'class-validator';

   export class CreateCatDto {
     @IsString()
     readonly name: string;

     @IsInt()
     @Min(0)
     @Max(30)
     readonly age: number;

     @IsString()
     readonly breed: string;
   }
   ```

2. **Aplicar Validaciones en el Controlador:**

   Utiliza el pipe de validación proporcionado por NestJS para aplicar las validaciones definidas en los DTOs.

   ```typescript
   import { Body, Controller, Post } from '@nestjs/common';
   import { CreateCatDto } from './dto/create-cat.dto';
   import { CatsService } from './cats.service';

   @Controller('cats')
   export class CatsController {
     constructor(private readonly catsService: CatsService) {}

     @Post()
     async create(@Body() createCatDto: CreateCatDto) {
       return this.catsService.create(createCatDto);
     }
   }
   ```

3. **Habilitar Validaciones Globales:**

   En el archivo `main.ts`, habilita el pipe de validación global para que todas las solicitudes pasen por las validaciones definidas en los DTOs.

   ```typescript
   import { ValidationPipe } from '@nestjs/common';
   import { NestFactory } from '@nestjs/core';
   import { AppModule } from './app.module';

   async function bootstrap() {
     const app = await NestFactory.create(AppModule);
     app.useGlobalPipes(new ValidationPipe());
     await app.listen(3000);
   }
   bootstrap();
   ```

### Ventajas de Usar Class Validator

- **Simplicidad:** Fácil de implementar y utilizar con decoradores.
- **Flexibilidad:** Soporta una amplia gama de validaciones personalizables.
- **Integración:** Se integra perfectamente con NestJS y su sistema de pipes.

---

## Conexión a Base de Datos

### Configuración de la Conexión con TypeORM

Para conectar NestJS con MySQL utilizando TypeORM, es necesario configurar los detalles de conexión en el módulo de TypeORM.

### Pasos para Configurar la Conexión

1. **Editar `app.module.ts`:**

   ```typescript
   import { Module } from '@nestjs/common';
   import { TypeOrmModule } from '@nestjs/typeorm';
   import { CatsModule } from './cats/cats.module';

   @Module({
     imports: [
       TypeOrmModule.forRoot({
         type: 'mysql',
         host: 'localhost',
         port: 3306,
         username: 'tu_usuario',
         password: 'tu_contraseña',
         database: 'nombre_de_la_base_de_datos',
         entities: [__dirname + '/**/*.entity{.ts,.js}'],
         synchronize: true,
       }),
       CatsModule,
     ],
     controllers: [],
     providers: [],
   })
   export class AppModule {}
   ```

   - **Type:** Tipo de base de datos (`mysql`).
   - **Host:** `localhost` si está ejecutándose localmente.
   - **Port:** Puerto de conexión (`3306` para MySQL).
   - **Username:** Usuario de la base de datos.
   - **Password:** Contraseña del usuario.
   - **Database:** Nombre de la base de datos.
   - **Entities:** Ruta donde se encuentran las entidades.
   - **Synchronize:** `true` para sincronizar automáticamente el esquema de la base de datos (solo en desarrollo).

### Beneficios de la Configuración

- **Facilidad de Uso:** TypeORM maneja la conexión y las operaciones básicas con la base de datos.
- **Automatización:** Las entidades se sincronizan automáticamente con el esquema de la base de datos.
- **Flexibilidad:** Permite configurar diferentes opciones según las necesidades del proyecto.

---

##  Repository Pattern

### ¿Qué es el Repository Pattern?

El **Repository Pattern** es un patrón de diseño que abstrae la lógica de acceso a datos, proporcionando una interfaz limpia para interactuar con la fuente de datos. En el contexto de TypeORM y NestJS, los repositorios gestionan las operaciones CRUD (Crear, Leer, Actualizar, Eliminar) para las entidades.

### Beneficios del Repository Pattern

- **Desacoplamiento:** Separa la lógica de acceso a datos de la lógica de negocio.
- **Mantenibilidad:** Facilita el mantenimiento y la escalabilidad del código.
- **Testabilidad:** Permite la creación de pruebas unitarias más fácilmente al mockear los repositorios.

### Implementación en NestJS

1. **Inyección del Repositorio:**

   En el servicio, inyecta el repositorio correspondiente a la entidad.

   ```typescript
   import { Injectable } from '@nestjs/common';
   import { InjectRepository } from '@nestjs/typeorm';
   import { Repository } from 'typeorm';
   import { Cat } from './entities/cat.entity';
   import { CreateCatDto } from './dto/create-cat.dto';

   @Injectable()
   export class CatsService {
     constructor(
       @InjectRepository(Cat)
       private catsRepository: Repository<Cat>,
     ) {}

     create(createCatDto: CreateCatDto): Promise<Cat> {
       const cat = this.catsRepository.create(createCatDto);
       return this.catsRepository.save(cat);
     }

     findAll(): Promise<Cat[]> {
       return this.catsRepository.find();
     }

     // Otros métodos CRUD
   }
   ```

2. **Uso del Repositorio:**

   Utiliza los métodos proporcionados por TypeORM para interactuar con la base de datos, como `find`, `findOne`, `create`, `save`, `remove`, etc.



---

##  Entity

### ¿Qué es una Entity en TypeORM?

Una **Entity** en TypeORM representa una tabla en la base de datos y cada instancia de la entidad representa una fila en dicha tabla. Las entidades se definen como clases de TypeScript decoradas con decoradores proporcionados por TypeORM.

### Definición de una Entity

1. **Crear la Clase de la Entity:**

   Crea un archivo `cat.entity.ts` en la carpeta `entities` dentro del módulo `cats`.

   ```typescript
   import { Entity, Column, PrimaryGeneratedColumn } from 'typeorm';

   @Entity()
   export class Cat {
     @PrimaryGeneratedColumn()
     id: number;

     @Column()
     name: string;

     @Column()
     age: number;

     @Column()
     breed: string;
   }
   ```

   - **@Entity():** Marca la clase como una entidad que TypeORM gestionará.
   - **@PrimaryGeneratedColumn():** Define la columna `id` como una clave primaria auto-generada.
   - **@Column():** Define las columnas de la entidad.

### Tipos de Columnas

- **Tipos Básicos:**
  - `string`, `number`, `boolean`, `Date`, etc.

- **Tipos Avanzados:**
  - `enum`, `array`, `json`, etc.

### Relaciones entre Entities

TypeORM permite definir relaciones entre entidades, como uno a uno, uno a muchos y muchos a muchos.

```typescript
import { Entity, Column, PrimaryGeneratedColumn, OneToMany } from 'typeorm';
import { Photo } from './photo.entity';

@Entity()
export class Cat {
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  name: string;

  @OneToMany(() => Photo, (photo) => photo.cat)
  photos: Photo[];
}
```

### Ventajas de Utilizar Entities

- **Mapeo Directo a la Base de Datos:** Facilita la sincronización entre el modelo de datos de la aplicación y la base de datos.
- **Organización:** Mantiene el código limpio y organizado al separar las definiciones de las entidades.
- **Flexibilidad:** Permite definir relaciones y tipos de columnas complejos.

---

##  Utilizando Repository Pattern

### Integración del Repository Pattern en el Servicio

Una vez definidas las entidades y configurado el repositorio, se pueden implementar métodos en el servicio para manejar las operaciones CRUD utilizando el Repository Pattern.

### Ejemplos de Métodos en el Servicio

1. **Crear un Nuevo Cat:**

   ```typescript
   async create(createCatDto: CreateCatDto): Promise<Cat> {
     const cat = this.catsRepository.create(createCatDto);
     return this.catsRepository.save(cat);
   }
   ```

   - **create:** Crea una nueva instancia de la entidad `Cat` con los datos proporcionados.
   - **save:** Persiste la entidad en la base de datos.

2. **Obtener Todos los Cats:**

   ```typescript
   findAll(): Promise<Cat[]> {
     return this.catsRepository.find();
   }
   ```

   - **find:** Recupera todas las entidades `Cat` de la base de datos.

3. **Obtener un Cat por ID:**

   ```typescript
   findOne(id: number): Promise<Cat> {
     return this.catsRepository.findOneBy({ id });
   }
   ```

   - **findOneBy:** Busca una entidad `Cat` específica por su `id`.

4. **Actualizar un Cat:**

   ```typescript
   async update(id: number, updateCatDto: UpdateCatDto): Promise<Cat> {
     await this.catsRepository.update(id, updateCatDto);
     return this.catsRepository.findOneBy({ id });
   }
   ```

   - **update:** Actualiza los datos de una entidad `Cat` existente.
   - **findOneBy:** Recupera la entidad actualizada.

5. **Eliminar un Cat:**

   ```typescript
   async remove(id: number): Promise<void> {
     await this.catsRepository.delete(id);
   }
   ```

   - **delete:** Elimina una entidad `Cat` de la base de datos.

### Beneficios de Utilizar Repository Pattern

- **Abstracción:** Oculta la complejidad de las operaciones de base de datos.
- **Reutilización de Código:** Permite reutilizar métodos y lógica de acceso a datos.
- **Facilidad de Pruebas:** Simplifica la creación de pruebas unitarias al permitir mockear repositorios.

---

## Create Cat DTO

### ¿Qué es un DTO?

**DTO (Data Transfer Object)** es un patrón de diseño que se utiliza para transferir datos entre diferentes capas de una aplicación. En NestJS, los DTOs se utilizan para definir la estructura de los datos que se envían y reciben a través de la API, asegurando que los datos cumplen con los requisitos antes de ser procesados.

### Creación de un CreateCatDto

1. **Definir el DTO:**

   Crea un archivo `create-cat.dto.ts` en la carpeta `dto` dentro del módulo `cats`.

   ```typescript
   import { IsString, IsInt, Min, Max } from 'class-validator';

   export class CreateCatDto {
     @IsString()
     readonly name: string;

     @IsInt()
     @Min(0)
     @Max(30)
     readonly age: number;

     @IsString()
     readonly breed: string;
   }
   ```

   - **Decoradores de Validación:**
     - `@IsString()`: Asegura que el valor es una cadena de texto.
     - `@IsInt()`: Asegura que el valor es un número entero.
     - `@Min()`, `@Max()`: Define los límites mínimo y máximo para el valor.

2. **Uso del DTO en el Controlador:**

   Aplica el DTO en el método `create` del controlador para validar los datos de entrada.

   ```typescript
   import { Body, Controller, Post } from '@nestjs/common';
   import { CreateCatDto } from './dto/create-cat.dto';
   import { CatsService } from './cats.service';

   @Controller('cats')
   export class CatsController {
     constructor(private readonly catsService: CatsService) {}

     @Post()
     async create(@Body() createCatDto: CreateCatDto) {
       return this.catsService.create(createCatDto);
     }
   }
   ```

### Ventajas de Usar DTOs

- **Validación de Datos:** Asegura que los datos recibidos cumplen con los requisitos antes de ser procesados.
- **Seguridad:** Previene la inyección de datos maliciosos al controlar la estructura y tipos de los datos.
- **Claridad:** Define claramente qué datos se esperan en cada operación, mejorando la mantenibilidad del código.

---

##  Soft Delete

### ¿Qué es Soft Delete?

**Soft Delete** es una técnica para eliminar registros de una base de datos sin borrarlos físicamente. En lugar de eliminar el registro, se marca como eliminado mediante un campo adicional, lo que permite restaurarlo en el futuro si es necesario.

### Implementación de Soft Delete con TypeORM

1. **Añadir una Columna de Eliminación Suave:**

   En la entidad `Cat`, añade un campo `deletedAt` que almacenará la fecha de eliminación.

   ```typescript
   import { Entity, Column, PrimaryGeneratedColumn, DeleteDateColumn } from 'typeorm';

   @Entity()
   export class Cat {
     @PrimaryGeneratedColumn()
     id: number;

     @Column()
     name: string;

     @Column()
     age: number;

     @Column()
     breed: string;

     @DeleteDateColumn()
     deletedAt?: Date;
   }
   ```

   - **@DeleteDateColumn():** Marca la columna para almacenar la fecha de eliminación suave.

2. **Configuración del Repositorio:**

   TypeORM maneja automáticamente las eliminaciones suaves si se usa el método `softDelete`.

   ```typescript
   async remove(id: number): Promise<void> {
     await this.catsRepository.softDelete(id);
   }
   ```

3. **Recuperar Registros Eliminados Suavemente:**

   Utiliza el método `restore` para recuperar un registro eliminado.

   ```typescript
   async restore(id: number): Promise<void> {
     await this.catsRepository.restore(id);
   }
   ```

4. **Filtrar Registros Eliminados:**

   Por defecto, TypeORM excluye los registros eliminados suavemente en las consultas. Para incluirlos, se puede usar el parámetro `withDeleted`.

   ```typescript
   findAll(): Promise<Cat[]> {
     return this.catsRepository.find({ withDeleted: true });
   }
   ```

### Ventajas de Soft Delete

- **Recuperación de Datos:** Permite restaurar registros eliminados por error.
- **Auditoría:** Mantiene un historial de registros eliminados.
- **Integridad Referencial:** Evita problemas en relaciones de tablas al no eliminar registros físicamente.

### Consideraciones

- **Rendimiento:** Puede afectar el rendimiento si se manejan grandes volúmenes de datos con muchos registros eliminados.
- **Mantenimiento:** Requiere limpieza periódica de registros eliminados para mantener la base de datos optimizada.

---

## Update

### Implementación de la Funcionalidad de Actualización

Actualizar registros en una API RESTful es una operación fundamental. En NestJS, esto se logra mediante la combinación de DTOs, validaciones y el uso del Repository Pattern.

### Pasos para Implementar la Actualización

1. **Crear el DTO de Actualización:**

   Define un DTO que permita actualizar campos específicos de la entidad `Cat`.

   ```typescript
   import { PartialType } from '@nestjs/mapped-types';
   import { CreateCatDto } from './create-cat.dto';

   export class UpdateCatDto extends PartialType(CreateCatDto) {}
   ```

   - **PartialType:** Permite que todos los campos del DTO original sean opcionales, facilitando actualizaciones parciales.

2. **Actualizar el Controlador:**

   Añade un método `update` en el controlador para manejar las solicitudes de actualización.

   ```typescript
   import { Body, Controller, Param, Patch } from '@nestjs/common';
   import { UpdateCatDto } from './dto/update-cat.dto';
   import { CatsService } from './cats.service';

   @Controller('cats')
   export class CatsController {
     constructor(private readonly catsService: CatsService) {}

     @Patch(':id')
     async update(@Param('id') id: number, @Body() updateCatDto: UpdateCatDto) {
       return this.catsService.update(id, updateCatDto);
     }
   }
   ```

3. **Actualizar el Servicio:**

   Implementa el método `update` en el servicio, utilizando el repositorio para actualizar el registro.

   ```typescript
   async update(id: number, updateCatDto: UpdateCatDto): Promise<Cat> {
     await this.catsRepository.update(id, updateCatDto);
     return this.catsRepository.findOneBy({ id });
   }
   ```

### Consideraciones para la Actualización

- **Validación de Datos:** Asegura que los datos de entrada cumplen con los requisitos antes de actualizar.
- **Manejo de Errores:** Gestiona adecuadamente los casos donde el registro a actualizar no existe.
- **Actualizaciones Parciales:** Permite actualizar solo los campos necesarios sin afectar otros datos.

---

## Relaciones SQL

### Introducción a las Relaciones en SQL

Las relaciones en bases de datos permiten asociar tablas entre sí, estableciendo cómo los datos en una tabla se relacionan con los datos en otra. Las relaciones principales son:

- **Uno a Uno (One-to-One):** Un registro en una tabla está asociado a un único registro en otra tabla.
- **Uno a Muchos (One-to-Many):** Un registro en una tabla está asociado a múltiples registros en otra tabla.
- **Muchos a Muchos (Many-to-Many):** Múltiples registros en una tabla están asociados a múltiples registros en otra tabla.

### Implementación de Relaciones con TypeORM

#### Relaciones Uno a Muchos

Ejemplo: Un `Cat` puede tener muchas `Photo`.

1. **Definir las Entidades:**

   ```typescript
   // cat.entity.ts
   import { Entity, Column, PrimaryGeneratedColumn, OneToMany } from 'typeorm';
   import { Photo } from './photo.entity';

   @Entity()
   export class Cat {
     @PrimaryGeneratedColumn()
     id: number;

     @Column()
     name: string;

     @OneToMany(() => Photo, (photo) => photo.cat)
     photos: Photo[];
   }
   ```

   ```typescript
   // photo.entity.ts
   import { Entity, Column, PrimaryGeneratedColumn, ManyToOne } from 'typeorm';
   import { Cat } from './cat.entity';

   @Entity()
   export class Photo {
     @PrimaryGeneratedColumn()
     id: number;

     @Column()
     url: string;

     @ManyToOne(() => Cat, (cat) => cat.photos)
     cat: Cat;
   }
   ```

2. **Gestión de las Relaciones:**

   - **Creación de Photos asociadas a un Cat:**
     - Al crear una `Photo`, se debe asociar al `Cat` correspondiente.
   - **Cascada de Operaciones:**
     - Configurar `cascade: true` si se desea que las operaciones en el `Cat` afecten automáticamente a las `Photos`.

#### Relaciones Muchos a Muchos

Ejemplo: Un `Cat` puede tener múltiples `Toys` y un `Toy` puede pertenecer a múltiples `Cats`.

1. **Definir las Entidades:**

   ```typescript
   // cat.entity.ts
   import { Entity, Column, PrimaryGeneratedColumn, ManyToMany, JoinTable } from 'typeorm';
   import { Toy } from './toy.entity';

   @Entity()
   export class Cat {
     @PrimaryGeneratedColumn()
     id: number;

     @Column()
     name: string;

     @ManyToMany(() => Toy, (toy) => toy.cats)
     @JoinTable()
     toys: Toy[];
   }
   ```

   ```typescript
   // toy.entity.ts
   import { Entity, Column, PrimaryGeneratedColumn, ManyToMany } from 'typeorm';
   import { Cat } from './cat.entity';

   @Entity()
   export class Toy {
     @PrimaryGeneratedColumn()
     id: number;

     @Column()
     name: string;

     @ManyToMany(() => Cat, (cat) => cat.toys)
     cats: Cat[];
   }
   ```

### Ventajas de Utilizar Relaciones en SQL

- **Normalización de Datos:** Evita la redundancia y asegura la integridad de los datos.
- **Eficiencia en Consultas:** Facilita la ejecución de consultas complejas y el filtrado de datos.
- **Flexibilidad:** Permite modelar relaciones complejas entre diferentes entidades.

### Consideraciones al Implementar Relaciones

- **Integridad Referencial:** Asegura que las relaciones entre tablas sean consistentes.
- **Optimización de Consultas:** Utiliza índices y optimiza las consultas para mejorar el rendimiento.
- **Manejo de Relaciones en el Código:** Gestiona adecuadamente las relaciones en el servicio y controlador para evitar errores y garantizar la consistencia de los datos.

---

##  Resumen

### Recapitulación de los Conceptos Clave

Durante esta primera semana, hemos abordado los fundamentos esenciales para construir una API RESTful utilizando NestJS, MySQL, TypeORM y TypeScript. A continuación, se resumen los puntos más importantes:

1. **Introducción a NestJS y su Ecosistema:**
   - Comprendimos qué es NestJS y por qué es una excelente elección para el desarrollo de aplicaciones backend.
   - Exploramos las ventajas de utilizar TypeScript junto con NestJS.

2. **TypeORM:**
   - Aprendimos qué es un ORM y cómo TypeORM facilita la interacción con bases de datos SQL.
   - Configuramos la conexión a MySQL y definimos entidades para mapear las tablas de la base de datos.

3. **Nest.js CLI:**
   - Instalamos y utilizamos el CLI de NestJS para generar módulos, controladores y servicios de manera eficiente.
   - Creamos el recurso `cats` utilizando el CLI, estableciendo una estructura coherente para la API.

4. **Docker Compose:**
   - Configuramos Docker Compose para gestionar contenedores de MySQL, asegurando un entorno de desarrollo consistente.
   - Iniciamos y gestionamos los servicios de Docker para mantener la base de datos en funcionamiento.

5. **Visualización de la Base de Datos:**
   - Instalamos y configuramos DBeaver para visualizar y gestionar la base de datos MySQL.
   - Exploramos las tablas, ejecutamos consultas y generamos diagramas ER para entender las relaciones entre entidades.

6. **Repository Pattern y Entities:**
   - Implementamos el Repository Pattern para abstraer la lógica de acceso a datos, mejorando la mantenibilidad y testabilidad del código.
   - Definimos entidades que representan las tablas de la base de datos, estableciendo relaciones entre ellas.

7. **Class Validator y DTOs:**
   - Utilizamos Class Validator para asegurar que los datos de entrada cumplen con los requisitos establecidos.
   - Creamos DTOs para definir la estructura de los datos que se transfieren a través de la API, mejorando la seguridad y consistencia.

8. **CRUD Operations:**
   - Implementamos las operaciones CRUD básicas (Crear, Leer, Actualizar, Eliminar) utilizando los servicios y controladores generados.
   - Aplicamos el Repository Pattern para manejar las operaciones de manera eficiente.

9. **Soft Delete:**
   - Implementamos la funcionalidad de Soft Delete para eliminar registros de manera lógica, permitiendo su recuperación en el futuro.
   - Gestionamos las eliminaciones y restauraciones de registros utilizando TypeORM.

10. **Relaciones SQL:**
    - Establecimos relaciones entre entidades, como uno a muchos y muchos a muchos, para modelar asociaciones complejas en la base de datos.
    - Configuramos las entidades y repositorios para manejar estas relaciones de manera coherente.

### Recursos Adicionales

- [Documentación Oficial de NestJS](https://docs.nestjs.com/)
- [Documentación Oficial de TypeORM](https://typeorm.io/)
- [Guía de Docker Compose](https://docs.docker.com/compose/)
- [DBeaver - Herramienta de Administración de Bases de Datos](https://dbeaver.io/)
- [Class Validator](https://github.com/typestack/class-validator)
- [Google Fonts](https://fonts.google.com/)
