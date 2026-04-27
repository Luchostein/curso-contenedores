# Curso Contenedores - API con NestJS

Proyecto backend construido con NestJS y TypeScript.

La aplicacion incluye:

- endpoints basicos de ejemplo
- modulo `calculo` para operaciones simples
- modulo `users-data` con soporte para PostgreSQL via TypeORM
- endpoints de health para liveness y readiness
- carga centralizada de configuracion desde variables de entorno

Este README describe solo el proyecto de aplicacion que vive en la raiz del repositorio.  
No cubre el material que esta dentro de `clase/`.

## Estructura principal

El codigo fuente vive en `src/`.

- [src/main.ts](src/main.ts): punto de entrada de NestJS
- [src/app.module.ts](src/app.module.ts): modulo principal
- [src/config/app.config.ts](src/config/app.config.ts): configuracion centralizada
- [src/modules/calculo](src/modules/calculo): modulo de calculo
- [src/modules/users-data](src/modules/users-data): modulo de usuarios y base de datos

## Requisitos

- Node.js 22+ o 24+
- npm

## Instalacion

Clona el repositorio y luego instala dependencias:

```bash
npm install
```

## Variables de entorno

La aplicacion usa estas variables:

- `PORT`: puerto HTTP de la app
- `ENABLE_DB`: activa o desactiva el modulo que usa base de datos
- `DB_HOST`: host de PostgreSQL
- `DB_PORT`: puerto de PostgreSQL
- `DB_USERNAME`: usuario de PostgreSQL
- `DB_PASSWORD`: password de PostgreSQL
- `DB_NAME`: nombre de la base de datos

Valores por defecto actuales:

- `PORT=3000`
- `ENABLE_DB=false`
- `DB_HOST=localhost`
- `DB_PORT=5432`
- `DB_USERNAME=postgres`
- `DB_PASSWORD=password`
- `DB_NAME=nestjs_db`

Si `ENABLE_DB=false`, la aplicacion arranca sin cargar el modulo de usuarios ni TypeORM.

## Levantar el proyecto

Modo normal:

```bash
npm run start
```

Modo desarrollo con recarga:

```bash
npm run start:dev
```

Modo debug:

```bash
npm run start:debug
```

Modo produccion:

```bash
npm run build
npm run start:prod
```

## Build

Compilar el proyecto:

```bash
npm run build
```

La salida compilada queda en `dist/`.

## Lint y pruebas

Ejecutar lint:

```bash
npm run lint
```

Ejecutar tests:

```bash
npm run test
```

Ejecutar tests con coverage:

```bash
npm run test:cov
```

## Endpoints principales

### Basicos

- `GET /hello`
- `GET /hi`

### Health

- `GET /health/live`
- `GET /health/ready`

`/health/live` sirve para saber si la app sigue viva.  
`/health/ready` sirve para saber si la app esta lista para recibir trafico.

Si la base de datos esta desactivada con `ENABLE_DB=false`, el readiness responde `ok` y marca la base como `skipped`.

### Pruebas de carga

- `GET /cpu`
- `GET /memory?size=100`

Estos endpoints existen para pruebas de consumo de CPU y memoria.

## Base de datos

El modulo de base de datos usa:

- NestJS Config
- TypeORM
- PostgreSQL

La conexion se configura en:

- [src/modules/users-data/database/database.module.ts](src/modules/users-data/database/database.module.ts)

Si quieres usar el modulo de usuarios, debes levantar PostgreSQL y definir:

```bash
ENABLE_DB=true
DB_HOST=localhost
DB_PORT=5432
DB_USERNAME=postgres
DB_PASSWORD=tu_password
DB_NAME=tu_base
```

## Ejemplo de arranque con base habilitada

```bash
ENABLE_DB=true \
DB_HOST=localhost \
DB_PORT=5432 \
DB_USERNAME=postgres \
DB_PASSWORD=postgres \
DB_NAME=curso_contenedores \
npm run start:dev
```

## Notas

- El proyecto esta pensado como backend de practica y demostracion.
- Hay archivos de infraestructura y ejemplos extra en `clase/`, pero no forman parte de este README.
