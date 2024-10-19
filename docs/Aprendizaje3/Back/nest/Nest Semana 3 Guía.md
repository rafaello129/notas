
# Autorización (Roles) con NestJS

Nos enfocaremos en la **autorización**, es decir, controlar el acceso a recursos según los **roles** de usuario.

---

## User Role y JWT Payload

### Añadiendo Roles a los Usuarios

Para implementar la autorización basada en roles, primero debemos asociar roles a nuestros usuarios.

#### Modificar la Entidad `User`

Agregamos una nueva propiedad `role` a nuestra entidad `User`.

**users/entities/user.entity.ts**

```typescript
import { Entity, PrimaryGeneratedColumn, Column } from 'typeorm';

@Entity()
export class User {
  @PrimaryGeneratedColumn()
  id: number;

  @Column({ unique: true })
  username: string;

  @Column()
  password: string;

  @Column({ default: 'user' })
  role: string;
}
```
- **`role`:** Indica el rol del usuario. Puede ser `'user'`, `'admin'`, etc.
- **`default: 'user'`:** Establece el rol por defecto como `'user'`.

### Incluyendo el Rol en el Payload del JWT

Cuando generamos el token JWT, podemos incluir información adicional en el **payload**.

#### Modificar el Método `login` en `AuthService`

**auth/auth.service.ts**

```typescript
async login(loginAuthDto: LoginAuthDto) {
  // ... Validación de credenciales

  const payload = { username: user.username, sub: user.id, role: user.role };
  return {
    access_token: this.jwtService.sign(payload),
  };
}
```

- **`role: user.role`:** Añadimos el rol del usuario al payload del token.

### Actualizar la Estrategia JWT

Necesitamos asegurarnos de que el rol esté disponible en el contexto de la solicitud.

**auth/jwt.strategy.ts**

```typescript
async validate(payload: any) {
  return { userId: payload.sub, username: payload.username, role: payload.role };
}
```

- Ahora, el objeto `req.user` incluirá `userId`, `username` y `role`.

---

## Verificación Manual de Rol Admin

### Control de Acceso en el Controlador

Podemos verificar el rol del usuario directamente en el controlador para proteger ciertas rutas.

#### Ejemplo en `CatsController`

**cats/cats.controller.ts**

```typescript
import { Controller, Get, UseGuards, Request, ForbiddenException } from '@nestjs/common';
import { JwtAuthGuard } from '../auth/jwt-auth.guard';

@Controller('cats')
export class CatsController {
  @UseGuards(JwtAuthGuard)
  @Get('admin')
  findAllAdmin(@Request() req) {
    if (req.user.role !== 'admin') {
      throw new ForbiddenException('Access denied');
    }
    // Código para usuarios con rol admin
    return this.catsService.findAll();
  }
}
```

- **Verificación del Rol:** Comprobamos si `req.user.role` es `'admin'`.
- **Manejo de Excepciones:** Si el rol no es `'admin'`, lanzamos una `ForbiddenException`.

### Limitaciones

- **Repetitivo:** Tener que verificar manualmente el rol en cada ruta puede ser tedioso y propenso a errores.
- **Mejoras:** Podemos crear un **Guard personalizado** para manejar esta lógica de manera centralizada.

---

## Decorador Personalizado

### Creando un Decorador `Roles`

Para simplificar la asignación de roles a las rutas, podemos crear un decorador personalizado.

#### Definir el Decorador `Roles`

**auth/roles.decorator.ts**

```typescript
import { SetMetadata } from '@nestjs/common';

export const ROLES_KEY = 'roles';
export const Roles = (...roles: string[]) => SetMetadata(ROLES_KEY, roles);
```

- **`SetMetadata`:** Función que asigna metadatos a una ruta.
- **`ROLES_KEY`:** Clave utilizada para acceder a los metadatos.
- **`Roles`:** Decorador que acepta una lista de roles.

### Uso del Decorador en el Controlador

**cats/cats.controller.ts**

```typescript
import { Controller, Get, UseGuards } from '@nestjs/common';
import { Roles } from '../auth/roles.decorator';
import { JwtAuthGuard } from '../auth/jwt-auth.guard';

@Controller('cats')
export class CatsController {
  @UseGuards(JwtAuthGuard)
  @Roles('admin')
  @Get('admin')
  findAllAdmin() {
    // Código para usuarios con rol admin
    return this.catsService.findAll();
  }
}
```

- **`@Roles('admin')`:** Especificamos que esta ruta requiere el rol `'admin'`.

### Necesidad de un Guard Personalizado

El decorador por sí solo no es suficiente; necesitamos un guard que interprete los metadatos y realice la verificación.

---

## Roles Guard

### Implementación del Guard de Roles

Crearemos un guard que verifique los roles antes de permitir el acceso a una ruta.

#### Definir el Guard `RolesGuard`

**auth/roles.guard.ts**

```typescript
import { Injectable, CanActivate, ExecutionContext } from '@nestjs/common';
import { Reflector } from '@nestjs/core';
import { ROLES_KEY } from './roles.decorator';

@Injectable()
export class RolesGuard implements CanActivate {
  constructor(private reflector: Reflector) {}

  canActivate(context: ExecutionContext): boolean {
    const requiredRoles = this.reflector.getAllAndOverride<string[]>(ROLES_KEY, [
      context.getHandler(),
      context.getClass(),
    ]);
    if (!requiredRoles) {
      return true; // Si no hay roles definidos, permitir acceso
    }
    const { user } = context.switchToHttp().getRequest();
    return requiredRoles.includes(user.role);
  }
}
```

- **`Reflector`:** Servicio para acceder a los metadatos.
- **`canActivate`:** Método que determina si el usuario tiene acceso.
- **`requiredRoles`:** Obtenemos los roles requeridos de los metadatos.

### Aplicación del Guard en el Controlador

**cats/cats.controller.ts**

```typescript
import { Controller, Get, UseGuards } from '@nestjs/common';
import { Roles } from '../auth/roles.decorator';
import { JwtAuthGuard } from '../auth/jwt-auth.guard';
import { RolesGuard } from '../auth/roles.guard';

@Controller('cats')
@UseGuards(JwtAuthGuard, RolesGuard)
export class CatsController {
  @Roles('admin')
  @Get('admin')
  findAllAdmin() {
    return this.catsService.findAll();
  }

  @Roles('user', 'admin')
  @Get()
  findAll() {
    return this.catsService.findAll();
  }
}
```

- **`@UseGuards(JwtAuthGuard, RolesGuard)`:** Aplica ambos guards a todas las rutas del controlador.
- **`@Roles(...)`:** Especifica los roles permitidos para cada ruta.

### Ventajas

- **Centralización:** La lógica de autorización está centralizada en el guard.
- **Reutilización:** Podemos aplicar el guard a múltiples controladores o rutas.

---

##  Enums en TypeScript

### Uso de Enums para Roles

Para evitar errores tipográficos y facilitar la gestión de roles, utilizamos **Enums** en TypeScript.

#### Definir el Enum `Role`

**auth/roles.enum.ts**

```typescript
export enum Role {
  User = 'user',
  Admin = 'admin',
}
```

### Actualizar el Decorador y el Guard

#### Modificar el Decorador `Roles`

**auth/roles.decorator.ts**

```typescript
import { SetMetadata } from '@nestjs/common';
import { Role } from './roles.enum';

export const Roles = (...roles: Role[]) => SetMetadata(ROLES_KEY, roles);
```

#### Modificar el Guard `RolesGuard`

El guard permanece igual, pero ahora trabaja con valores del enum.

### Actualizar el Controlador

**cats/cats.controller.ts**

```typescript
import { Controller, Get, UseGuards } from '@nestjs/common';
import { Roles } from '../auth/roles.decorator';
import { JwtAuthGuard } from '../auth/jwt-auth.guard';
import { RolesGuard } from '../auth/roles.guard';
import { Role } from '../auth/roles.enum';

@Controller('cats')
@UseGuards(JwtAuthGuard, RolesGuard)
export class CatsController {
  @Roles(Role.Admin)
  @Get('admin')
  findAllAdmin() {
    return this.catsService.findAll();
  }

  @Roles(Role.User, Role.Admin)
  @Get()
  findAll() {
    return this.catsService.findAll();
  }
}
```

- **Uso del Enum:** Utilizamos `Role.Admin` y `Role.User` en lugar de cadenas de texto.

---

## Unir Varios Decoradores

### Combinación de Decoradores

Para simplificar aún más, podemos crear un decorador que combine la aplicación de los guards y la asignación de roles.

#### Crear un Decorador `Auth`

**auth/auth.decorator.ts**

```typescript
import { applyDecorators, UseGuards } from '@nestjs/common';
import { Roles } from './roles.decorator';
import { JwtAuthGuard } from './jwt-auth.guard';
import { RolesGuard } from './roles.guard';

export function Auth(...roles: Role[]) {
  return applyDecorators(
    Roles(...roles),
    UseGuards(JwtAuthGuard, RolesGuard),
  );
}
```

- **`applyDecorators`:** Permite combinar múltiples decoradores en uno solo.

### Uso del Decorador `Auth`

**cats/cats.controller.ts**

```typescript
import { Controller, Get } from '@nestjs/common';
import { Auth } from '../auth/auth.decorator';
import { Role } from '../auth/roles.enum';

@Controller('cats')
export class CatsController {
  @Auth(Role.Admin)
  @Get('admin')
  findAllAdmin() {
    return this.catsService.findAll();
  }

  @Auth(Role.User, Role.Admin)
  @Get()
  findAll() {
    return this.catsService.findAll();
  }
}
```

- Ahora, con un solo decorador, aplicamos la autenticación y autorización.

---
## Ocultar Contraseña

### Excluir la Contraseña al Devolver el Usuario

Es una mala práctica devolver la contraseña (aunque esté hasheada) en las respuestas de la API.

#### Utilizar Exclude de `class-transformer`

**users/entities/user.entity.ts**

```typescript
import { Exclude } from 'class-transformer';

@Entity()
export class User {
  // ...

  @Exclude()
  @Column()
  password: string;
}
```

- **`@Exclude()`:** Indica que esta propiedad debe excluirse al transformar la entidad en JSON.

### Aplicar Transformación en el Servicio

En los métodos que devuelven usuarios, utilizamos `class-transformer` para aplicar la exclusión.

**users/users.service.ts**

```typescript
import { instanceToPlain } from 'class-transformer';

async findOne(username: string): Promise<User | undefined> {
  const user = await this.usersRepository.findOneBy({ username });
  return user ? instanceToPlain(user) : undefined;
}
```

---

## Enum Roles en Entidad

### Definir el Tipo de Datos de `role` en la Entidad

Podemos indicar que el campo `role` acepta solo valores definidos en el enum.

**users/entities/user.entity.ts**

```typescript
import { Role } from '../../auth/roles.enum';

@Entity()
export class User {
  // ...

  @Column({
    type: 'enum',
    enum: Role,
    default: Role.User,
  })
  role: Role;
}
```

- **`type: 'enum'`:** Indica que el campo es de tipo enum en la base de datos.
- **`enum: Role`:** Especifica el enum a utilizar.

### Ventajas

- **Integridad de Datos:** La base de datos solo aceptará valores definidos en el enum.
- **Consistencia:** Facilita el mantenimiento y reduce errores.

---

## Rol Admin con Privilegios

### Implementación de Privilegios para el Rol Admin

Ahora, aseguraremos que solo los usuarios con rol `admin` puedan acceder a ciertos recursos, como la creación de nuevos roles o la gestión de usuarios.

#### Proteger Rutas con el Decorador `Auth`

**users/users.controller.ts**

```typescript
import { Controller, Get, Post, Body } from '@nestjs/common';
import { UsersService } from './users.service';
import { Auth } from '../auth/auth.decorator';
import { Role } from '../auth/roles.enum';

@Controller('users')
export class UsersController {
  constructor(private usersService: UsersService) {}

  @Auth(Role.Admin)
  @Get()
  findAll() {
    return this.usersService.findAll();
  }

  @Auth(Role.Admin)
  @Post()
  create(@Body() createUserDto: CreateUserDto) {
    return this.usersService.create(createUserDto);
  }
}
```

- **Solo Admin:** Solo usuarios con rol `admin` pueden acceder a estas rutas.

---

## Decorador Request User

### Creando un Decorador `User`

Para acceder al usuario autenticado de manera más sencilla, podemos crear un decorador personalizado.

#### Definir el Decorador `User`

**auth/user.decorator.ts**

```typescript
import { createParamDecorator, ExecutionContext } from '@nestjs/common';

export const User = createParamDecorator(
  (data, ctx: ExecutionContext) => {
    const request = ctx.switchToHttp().getRequest();
    return request.user;
  },
);
```

- **`createParamDecorator`:** Crea un decorador de parámetros.
- **`request.user`:** Accedemos al usuario autenticado.

### Uso del Decorador en el Controlador

**cats/cats.controller.ts**

```typescript
import { Controller, Get } from '@nestjs/common';
import { Auth } from '../auth/auth.decorator';
import { User } from '../auth/user.decorator';

@Controller('cats')
export class CatsController {
  @Auth()
  @Get('profile')
  getProfile(@User() user) {
    return user;
  }
}
```

- **`@User() user`:** Inyecta el usuario autenticado en el parámetro `user`.

---

## Breed Solo Rol Admin

### Control de Acceso en Operaciones Específicas

Podemos restringir ciertas operaciones, como la creación de nuevas razas (`breed`), solo a usuarios con rol `admin`.

#### Definir el Módulo `Breeds`

Supongamos que tenemos un módulo `Breeds` para gestionar las razas de gatos.

**breeds/breeds.controller.ts**

```typescript
import { Controller, Post, Body } from '@nestjs/common';
import { Auth } from '../auth/auth.decorator';
import { Role } from '../auth/roles.enum';

@Controller('breeds')
export class BreedsController {
  @Auth(Role.Admin)
  @Post()
  create(@Body() createBreedDto: CreateBreedDto) {
    // Lógica para crear una nueva raza
  }
}
```

- **Restricción a Admin:** Solo los administradores pueden crear nuevas razas.

---

## Relación entre Cat y User

### Asociar los Gatos (`Cat`) con el Usuario que los Crea

Queremos que cada gato registrado esté asociado al usuario que lo creó.

#### Modificar la Entidad `Cat`

**cats/entities/cat.entity.ts**

```typescript
import { Entity, Column, PrimaryGeneratedColumn, ManyToOne } from 'typeorm';
import { User } from '../../users/entities/user.entity';

@Entity()
export class Cat {
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  name: string;

  // Otras propiedades

  @ManyToOne(() => User, (user) => user.cats)
  owner: User;
}
```

- **`@ManyToOne`:** Indica una relación de muchos a uno con `User`.
- **`owner`:** Propiedad que referencia al usuario propietario del gato.

#### Modificar la Entidad `User`

**users/entities/user.entity.ts**

```typescript
import { OneToMany } from 'typeorm';
import { Cat } from '../../cats/entities/cat.entity';

@Entity()
export class User {
  // ...

  @OneToMany(() => Cat, (cat) => cat.owner)
  cats: Cat[];
}
```

- **`@OneToMany`:** Indica que un usuario puede tener muchos gatos.

### Actualizar el Método `create` en `CatsService`

**cats/cats.service.ts**

```typescript
async create(createCatDto: CreateCatDto, user: User): Promise<Cat> {
  const cat = this.catsRepository.create({ ...createCatDto, owner: user });
  return this.catsRepository.save(cat);
}
```

- Asociamos el gato creado con el usuario que lo creó.

### Actualizar el Controlador

**cats/cats.controller.ts**

```typescript
import { Controller, Post, Body } from '@nestjs/common';
import { Auth } from '../auth/auth.decorator';
import { User } from '../auth/user.decorator';

@Controller('cats')
export class CatsController {
  @Auth()
  @Post()
  create(@Body() createCatDto: CreateCatDto, @User() user: User) {
    return this.catsService.create(createCatDto, user);
  }
}
```

- Inyectamos el usuario autenticado y lo pasamos al servicio.

---

## Métodos findAll Cat

### Filtrar Gatos por Usuario

Queremos que los usuarios solo puedan ver los gatos que ellos mismos crearon, a menos que sean administradores.

#### Modificar el Método `findAll` en `CatsService`

**cats/cats.service.ts**

```typescript
async findAll(user: User): Promise<Cat[]> {
  if (user.role === Role.Admin) {
    return this.catsRepository.find({ relations: ['owner'] });
  }
  return this.catsRepository.find({
    where: { owner: { id: user.id } },
    relations: ['owner'],
  });
}
```

- **Admin:** Si el usuario es admin, devuelve todos los gatos.
- **Usuario Regular:** Devuelve solo los gatos que pertenecen al usuario.

### Actualizar el Controlador

**cats/cats.controller.ts**

```typescript
@Auth()
@Get()
findAll(@User() user: User) {
  return this.catsService.findAll(user);
}
```

---

## Método findOne Cat

### Restringir Acceso al Método `findOne`

Al obtener un gato por ID, debemos asegurarnos de que el usuario tenga permiso para verlo.

#### Modificar el Método `findOne` en `CatsService`

**cats/cats.service.ts**

```typescript
async findOne(id: number, user: User): Promise<Cat> {
  const cat = await this.catsRepository.findOne({
    where: { id },
    relations: ['owner'],
  });
  if (!cat) {
    throw new NotFoundException('Cat not found');
  }
  if (user.role !== Role.Admin && cat.owner.id !== user.id) {
    throw new ForbiddenException('Access denied');
  }
  return cat;
}
```

- **Verificación de Propiedad:** Si el usuario no es el propietario y no es admin, se deniega el acceso.

### Actualizar el Controlador

**cats/cats.controller.ts**

```typescript
@Auth()
@Get(':id')
findOne(@Param('id') id: number, @User() user: User) {
  return this.catsService.findOne(+id, user);
}
```

---

## Actualizar Cat

### Control de Acceso en Actualización

Solo el propietario o un administrador pueden actualizar un gato.

#### Modificar el Método `update` en `CatsService`

**cats/cats.service.ts**

```typescript
async update(id: number, updateCatDto: UpdateCatDto, user: User): Promise<Cat> {
  const cat = await this.findOne(id, user);
  Object.assign(cat, updateCatDto);
  return this.catsRepository.save(cat);
}
```

- **Reutilizamos `findOne`:** Garantiza que el usuario tiene permiso para actualizar.
- **Actualización:** Modificamos los campos y guardamos.

### Actualizar el Controlador

**cats/cats.controller.ts**

```typescript
@Auth()
@Patch(':id')
update(@Param('id') id: number, @Body() updateCatDto: UpdateCatDto, @User() user: User) {
  return this.catsService.update(+id, updateCatDto, user);
}
```

---

## Eliminar Cat

### Control de Acceso en Eliminación

Solo el propietario o un administrador pueden eliminar un gato.

#### Modificar el Método `remove` en `CatsService`

**cats/cats.service.ts**

```typescript
async remove(id: number, user: User): Promise<void> {
  const cat = await this.findOne(id, user);
  await this.catsRepository.remove(cat);
}
```

- **Verificación de Permisos:** Utilizamos `findOne` para validar.
- **Eliminación:** Eliminamos el registro de la base de datos.

### Actualizar el Controlador

**cats/cats.controller.ts**

```typescript
@Auth()
@Delete(':id')
remove(@Param('id') id: number, @User() user: User) {
  return this.catsService.remove(+id, user);
}
```
