# Semana 2: Autenticación y Autorización con NestJS

- **Autenticación**: Proceso de verificar la identidad del usuario. Asegura que quien intenta acceder es quien dice ser.
- **Autorización**: Proceso de verificar los permisos del usuario autenticado para acceder a recursos específicos.

---

## Módulo de Usuarios (Users)

Para manejar la autenticación, necesitamos un módulo que gestione a los usuarios de nuestra aplicación.

### Creación del Módulo

Utilizaremos el CLI de NestJS para generar el módulo de usuarios:

```bash
nest generate module users
```
Esto crea un archivo `users.module.ts` que será el núcleo de nuestro módulo de usuarios.

### Definición de la Entidad Usuario

Crearemos una entidad `User` que representará a los usuarios en nuestra base de datos.

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
}
```

- **Decoradores de TypeORM**:
  - `@Entity()`: Indica que esta clase es una entidad de base de datos.
  - `@PrimaryGeneratedColumn()`: Clave primaria autogenerada.
  - `@Column()`: Define una columna en la tabla.
- **Propiedades**:
  - `username`: Nombre de usuario único.
  - `password`: Contraseña del usuario (será almacenada de forma segura).

### Implementación del Servicio de Usuarios

Creamos un servicio para manejar la lógica de negocio relacionada con los usuarios.

**Generar el servicio**:

```bash
nest generate service users
```

**users/users.service.ts**

```typescript
import { Injectable } from '@nestjs/common';
import { InjectRepository } from '@nestjs/typeorm';
import { Repository } from 'typeorm';
import { User } from './entities/user.entity';

@Injectable()
export class UsersService {
  constructor(
    @InjectRepository(User)
    private usersRepository: Repository<User>,
  ) {}

  async findOne(username: string): Promise<User | undefined> {
    return this.usersRepository.findOneBy({ username });
  }

  async create(user: Partial<User>): Promise<User> {
    const newUser = this.usersRepository.create(user);
    return this.usersRepository.save(newUser);
  }

  // Otros métodos según sea necesario
}
```

- **Inyección del Repositorio**: Utilizamos `@InjectRepository` para acceder al repositorio de la entidad `User`.
- **Métodos del Servicio**:
  - `findOne()`: Busca un usuario por nombre de usuario.
  - `create()`: Crea un nuevo usuario.

### Actualización del Módulo de Usuarios

Debemos importar el `TypeOrmModule` en `users.module.ts` para que el repositorio esté disponible.

**users/users.module.ts**

```typescript
import { Module } from '@nestjs/common';
import { TypeOrmModule } from '@nestjs/typeorm';
import { UsersService } from './users.service';
import { User } from './entities/user.entity';

@Module({
  imports: [TypeOrmModule.forFeature([User])],
  providers: [UsersService],
  exports: [UsersService],
})
export class UsersModule {}
```

- **imports**: Importamos `TypeOrmModule.forFeature([User])` para registrar el repositorio de `User`.
- **exports**: Exportamos `UsersService` para que pueda ser utilizado en otros módulos.

---

## Módulo de Autenticación (Auth)

Crearemos un módulo dedicado a la autenticación que gestionará el proceso de login y registro.

### Creación del Módulo y Controlador

Utilizamos el CLI de NestJS para generar el módulo y el controlador de autenticación:

```bash
nest generate module auth
nest generate controller auth
nest generate service auth
```

Esto crea los archivos `auth.module.ts`, `auth.controller.ts` y `auth.service.ts`.

### Configuración de Dependencias

En `auth.module.ts`, importamos el módulo de usuarios y otros módulos necesarios:

**auth/auth.module.ts**

```typescript
import { Module } from '@nestjs/common';
import { UsersModule } from '../users/users.module';
import { AuthService } from './auth.service';
import { AuthController } from './auth.controller';

@Module({
  imports: [UsersModule],
  providers: [AuthService],
  controllers: [AuthController],
})
export class AuthModule {}
```

- **imports**: Importamos `UsersModule` para acceder al servicio de usuarios.
- **providers**: Registramos `AuthService`.
- **controllers**: Registramos `AuthController`.

---

## Registro de Usuarios (Register)

Implementaremos la funcionalidad para que nuevos usuarios puedan registrarse en nuestra aplicación.

### Creación del DTO de Registro

Definimos un DTO (Data Transfer Object) para validar los datos de registro.

**auth/dto/register-auth.dto.ts**

```typescript
import { IsString, MinLength } from 'class-validator';

export class RegisterAuthDto {
  @IsString()
  username: string;

  @IsString()
  @MinLength(6)
  password: string;
}
```

- **Decoradores de Validación**:
  - `@IsString()`: Valida que el campo sea una cadena de texto.
  - `@MinLength(6)`: Valida que la contraseña tenga al menos 6 caracteres.

### Implementación del Método de Registro

En `AuthService`, creamos un método `register` que utiliza `UsersService` para crear un nuevo usuario.

**auth/auth.service.ts**

```typescript
import { Injectable } from '@nestjs/common';
import { UsersService } from '../users/users.service';
import { RegisterAuthDto } from './dto/register-auth.dto';

@Injectable()
export class AuthService {
  constructor(private usersService: UsersService) {}

  async register(registerAuthDto: RegisterAuthDto) {
    const userExists = await this.usersService.findOne(registerAuthDto.username);
    if (userExists) {
      throw new Error('El usuario ya existe');
    }
    return this.usersService.create(registerAuthDto);
  }
}
```

- **Validación de Usuario Existente**: Verificamos si el nombre de usuario ya está en uso.
- **Creación del Usuario**: Utilizamos `usersService.create` para crear el nuevo usuario.

En `AuthController`, creamos el endpoint para el registro.

**auth/auth.controller.ts**

```typescript
import { Controller, Post, Body } from '@nestjs/common';
import { AuthService } from './auth.service';
import { RegisterAuthDto } from './dto/register-auth.dto';

@Controller('auth')
export class AuthController {
  constructor(private authService: AuthService) {}

  @Post('register')
  async register(@Body() registerAuthDto: RegisterAuthDto) {
    return this.authService.register(registerAuthDto);
  }
}
```

- **Endpoint `/auth/register`**: Maneja las solicitudes POST para registrar nuevos usuarios.

---

## Hash de Contraseña

Es fundamental no almacenar contraseñas en texto plano por razones de seguridad. Utilizaremos **bcrypt** para encriptar las contraseñas antes de guardarlas.

### Uso de Bcrypt

**Instalación**:

```bash
npm install bcrypt
npm install -D @types/bcrypt
```

### Implementación del Hashing

Modificamos el método `register` en `AuthService` para hashear la contraseña.

**auth/auth.service.ts**

```typescript
import * as bcrypt from 'bcrypt';

@Injectable()
export class AuthService {
  // ...

  async register(registerAuthDto: RegisterAuthDto) {
    const { username, password } = registerAuthDto;
    const userExists = await this.usersService.findOne(username);
    if (userExists) {
      throw new Error('El usuario ya existe');
    }
    const hashedPassword = await bcrypt.hash(password, 10);
    return this.usersService.create({
      username,
      password: hashedPassword,
    });
  }
}
```

- **bcrypt.hash()**: Genera un hash seguro de la contraseña con un salt de 10 rondas.
- **Almacenamiento Seguro**: Solo guardamos el hash de la contraseña en la base de datos.

---

## Autenticación (Login)

Implementaremos el proceso de login, validando las credenciales del usuario.

### Creación del DTO de Login

Definimos un DTO para validar los datos de login.

**auth/dto/login-auth.dto.ts**

```typescript
import { IsString } from 'class-validator';

export class LoginAuthDto {
  @IsString()
  username: string;

  @IsString()
  password: string;
}
```

### Validación de Credenciales

En `AuthService`, creamos el método `login` que verifica las credenciales del usuario.

**auth/auth.service.ts**

```typescript
async login(loginAuthDto: LoginAuthDto) {
  const { username, password } = loginAuthDto;
  const user = await this.usersService.findOne(username);
  if (!user) {
    throw new Error('Usuario no encontrado');
  }
  const isMatch = await bcrypt.compare(password, user.password);
  if (!isMatch) {
    throw new Error('Contraseña incorrecta');
  }
  // Generar y devolver un token (JWT)
}
```

- **bcrypt.compare()**: Compara la contraseña proporcionada con el hash almacenado.
- **Validación de Usuario y Contraseña**: Asegura que las credenciales sean correctas antes de proceder.

En `AuthController`, creamos el endpoint para el login.

**auth/auth.controller.ts**

```typescript
@Post('login')
async login(@Body() loginAuthDto: LoginAuthDto) {
  return this.authService.login(loginAuthDto);
}
```

---

## JWT (JSON Web Tokens)

Utilizaremos JWT para generar tokens que permitan a los usuarios autenticarse y acceder a recursos protegidos.

### Configuración del Módulo JWT

**Instalación**:

```bash
npm install @nestjs/jwt passport-jwt
npm install -D @types/passport-jwt
```

En `auth.module.ts`, importamos y configuramos el módulo JWT.

**auth/auth.module.ts**

```typescript
import { JwtModule } from '@nestjs/jwt';

@Module({
  imports: [
    UsersModule,
    JwtModule.register({
      secret: 'SECRET_KEY', // Reemplazar por una clave más segura y almacenarla en variables de entorno
      signOptions: { expiresIn: '1h' },
    }),
  ],
  // ...
})
export class AuthModule {}
```

- **secret**: Clave secreta para firmar los tokens (debe ser segura y estar en variables de entorno).
- **signOptions**: Opciones como tiempo de expiración del token.

### Generación de Tokens

Modificamos el método `login` para generar y devolver un token JWT.

**auth/auth.service.ts**

```typescript
import { JwtService } from '@nestjs/jwt';

@Injectable()
export class AuthService {
  constructor(
    private usersService: UsersService,
    private jwtService: JwtService,
  ) {}

  async login(loginAuthDto: LoginAuthDto) {
    // ... Validación de credenciales

    const payload = { username: user.username, sub: user.id };
    return {
      access_token: this.jwtService.sign(payload),
    };
  }
}
```

- **jwtService.sign()**: Genera un token JWT con el payload proporcionado.
- **Payload**: Información que se incluye en el token (evitar información sensible).

---

## Autorización (Guard)

Para proteger rutas y asegurarnos de que solo usuarios autenticados accedan a ciertos recursos, utilizaremos Guards.

### Implementación de Guards

NestJS utiliza **Passport** para manejar la autenticación con JWT.

**Instalación**:

```bash
npm install passport
npm install @nestjs/passport
```

Creamos un guard que utilice la estrategia de JWT.

**auth/jwt-auth.guard.ts**

```typescript
import { Injectable } from '@nestjs/common';
import { AuthGuard } from '@nestjs/passport';

@Injectable()
export class JwtAuthGuard extends AuthGuard('jwt') {}
```

Definimos la estrategia JWT.

**auth/jwt.strategy.ts**

```typescript
import { Injectable } from '@nestjs/common';
import { PassportStrategy } from '@nestjs/passport';
import { Strategy, ExtractJwt } from 'passport-jwt';

@Injectable()
export class JwtStrategy extends PassportStrategy(Strategy) {
  constructor() {
    super({
      jwtFromRequest: ExtractJwt.fromAuthHeaderAsBearerToken(),
      ignoreExpiration: false,
      secretOrKey: 'SECRET_KEY', // Debe coincidir con la clave usada para firmar
    });
  }

  async validate(payload: any) {
    return { userId: payload.sub, username: payload.username };
  }
}
```

- **jwtFromRequest**: Especifica cómo extraer el token de la solicitud (en este caso, del encabezado `Authorization`).
- **validate()**: Método que verifica el token y devuelve los datos del usuario.

### Protección de Rutas

En `cats.controller.ts`, protegemos las rutas utilizando el guard.

**cats/cats.controller.ts**

```typescript
import { Controller, Get, UseGuards } from '@nestjs/common';
import { JwtAuthGuard } from '../auth/jwt-auth.guard';

@Controller('cats')
export class CatsController {
  // ...

  @UseGuards(JwtAuthGuard)
  @Get()
  findAll() {
    // Solo usuarios autenticados pueden acceder
    return this.catsService.findAll();
  }
}
```

- **@UseGuards(JwtAuthGuard)**: Indica que esta ruta está protegida y requiere autenticación.

---
### Recursos Adicionales

- [Documentación Oficial de NestJS](https://docs.nestjs.com/)
- [Passport y JWT en NestJS](https://docs.nestjs.com/security/authentication)
- [TypeORM Relations](https://typeorm.io/#/relations)
- [Bcrypt Documentation](https://www.npmjs.com/package/bcrypt)

