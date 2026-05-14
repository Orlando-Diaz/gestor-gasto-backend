# 🗄️ Gestor de Gastos - Backend API

Backend API REST desarrollado con Node.js + Express + PostgreSQL para la aplicación móvil de gestión de gastos personales.

---

## 📋 Tabla de Contenidos

1. [Estado del Proyecto](#-estado-del-proyecto)
2. [Stack Tecnológico](#-stack-tecnológico)
3. [Requisitos Previos](#-requisitos-previos)
4. [Instalación y Configuración](#-instalación-y-configuración)
5. [Variables de Entorno](#-variables-de-entorno)
6. [Estructura del Proyecto](#-estructura-del-proyecto)
7. [Scripts Disponibles](#-scripts-disponibles)
8. [Endpoints de la API](#-endpoints-de-la-api)
9. [Base de Datos](#-base-de-datos)
10. [Próximos Pasos](#-próximos-pasos)
11. [Progreso de Desarrollo](#-progreso-de-desarrollo)
12. [Troubleshooting](#-troubleshooting)

---

## 🚀 Estado del Proyecto

**Versión:** 1.0.0 (En Desarrollo)

**Fecha de Inicio:** Mayo 2026

### ✅ Completado
- [x] Inicialización del proyecto Node.js
- [x] Configuración de Express
- [x] Middlewares de seguridad (Helmet, CORS)
- [x] Estructura de carpetas profesional
- [x] Variables de entorno configuradas
- [x] Servidor corriendo en puerto 3000
- [x] PostgreSQL instalado y funcionando
- [x] Base de datos `gestor_gastos_db` creada
- [x] Repositorio en GitHub

### 🔄 En Progreso
- [ ] Configuración de Sequelize (ORM)
- [ ] Modelos de base de datos
- [ ] Endpoints de autenticación
- [ ] Sistema JWT

### 📋 Pendiente
- [ ] Endpoints de transacciones
- [ ] Endpoints de categorías
- [ ] Endpoints de presupuestos
- [ ] Endpoints de estadísticas
- [ ] Testing
- [ ] Documentación de API completa
- [ ] Deploy en producción

---

## 🛠️ Stack Tecnológico

### Runtime & Framework
- **Node.js** v18+ LTS
- **Express.js** v4.21.2 - Framework web

### Base de Datos
- **PostgreSQL** v18 - Base de datos relacional
- **Sequelize** v6.37.5 - ORM para PostgreSQL

### Autenticación & Seguridad
- **bcryptjs** v2.4.3 - Hash de contraseñas
- **jsonwebtoken** v9.0.2 - Tokens JWT
- **helmet** v8.0.0 - Seguridad HTTP headers
- **cors** v2.8.5 - Cross-Origin Resource Sharing

### Validación & Utilidades
- **express-validator** v7.2.1 - Validación de requests
- **dotenv** v16.4.7 - Variables de entorno
- **morgan** v1.10.0 - Logging de requests

### Desarrollo
- **nodemon** v3.1.9 - Auto-restart del servidor

---

## 📦 Requisitos Previos

Antes de comenzar, asegúrate de tener instalado:

- **Node.js** v18 o superior ([Descargar](https://nodejs.org/))
- **PostgreSQL** v15 o superior ([Descargar](https://www.postgresql.org/download/))
- **Git** ([Descargar](https://git-scm.com/))
- **pgAdmin 4** (incluido con PostgreSQL) - Cliente gráfico para BD

**Editores recomendados:**
- Visual Studio Code
- IntelliJ IDEA
- WebStorm

---

## 🚀 Instalación y Configuración

### 1. Clonar el Repositorio

```bash
git clone https://github.com/Orlando-Diaz/gestor-gasto-backend.git
cd gestor-gasto-backend
```

### 2. Instalar Dependencias

```bash
npm install
```

Esto instalará todas las dependencias especificadas en `package.json`.

### 3. Configurar Variables de Entorno

Copia el archivo `.env.example` y renómbralo a `.env`:

```bash
cp .env.example .env
```

Luego edita `.env` con tus credenciales (ver sección de Variables de Entorno).

### 4. Verificar PostgreSQL

Asegúrate de que PostgreSQL esté corriendo:

**Windows:**
```bash
# Verificar servicio
Get-Service -Name postgresql-x64-18

# Iniciar si está detenido
Start-Service -Name postgresql-x64-18
```

**Linux/Mac:**
```bash
# Verificar estado
sudo systemctl status postgresql

# Iniciar si está detenido
sudo systemctl start postgresql
```

### 5. Crear Base de Datos

Opción A - Desde pgAdmin:
1. Abrir pgAdmin 4
2. Conectarse al servidor PostgreSQL
3. Click derecho en "Databases" → Create → Database
4. Nombre: `gestor_gastos_db`
5. Owner: `postgres`
6. Save

Opción B - Desde psql:
```bash
psql -U postgres
CREATE DATABASE gestor_gastos_db;
\q
```

### 6. Iniciar el Servidor

**Desarrollo (con auto-reload):**
```bash
npm run dev
```

**Producción:**
```bash
npm start
```

Deberías ver:
```
🚀 Servidor corriendo en puerto 3000
📍 http://localhost:3000
🌍 Entorno: development
```

### 7. Probar la API

Abre tu navegador y ve a:
```
http://localhost:3000
```

Deberías ver:
```json
{
  "success": true,
  "message": "✅ API de Gestor de Gastos funcionando correctamente",
  "version": "1.0.0",
  "timestamp": "2026-05-14T..."
}
```

---

## ⚙️ Variables de Entorno

El archivo `.env` contiene configuraciones sensibles. **NUNCA** lo subas a Git.

### Configuración Requerida

```env
# ============================================
# SERVIDOR
# ============================================
PORT=3000
NODE_ENV=development

# ============================================
# BASE DE DATOS (PostgreSQL)
# ============================================
DB_HOST=localhost
DB_PORT=5432
DB_NAME=gestor_gastos_db
DB_USER=postgres
DB_PASSWORD=tu_contraseña_aqui

# ============================================
# JWT (Autenticación)
# ============================================
JWT_SECRET=tu_super_secreto_jwt_cambialo_en_produccion_123456789
JWT_EXPIRES_IN=7d

# ============================================
# EMAIL (Opcional - para recuperación de contraseña)
# ============================================
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USER=tu_email@gmail.com
EMAIL_PASSWORD=tu_password_de_aplicacion
```

### ⚠️ Notas Importantes

1. **`DB_PASSWORD`**: Reemplaza con la contraseña que configuraste al instalar PostgreSQL
2. **`JWT_SECRET`**: En producción, usa una cadena aleatoria de al menos 32 caracteres
3. **`EMAIL_PASSWORD`**: Si usas Gmail, necesitas una "Contraseña de aplicación" (no tu contraseña normal)

### 🔒 Seguridad

- El archivo `.env` está en `.gitignore` (no se sube a GitHub)
- `.env.example` es la plantilla (sí se sube a GitHub)
- En producción, usa variables de entorno del servidor (Heroku, Railway, etc.)

---

## 📁 Estructura del Proyecto

```
gestor-gasto-backend/
│
├── src/                          # Código fuente
│   ├── config/                   # Configuraciones
│   │   ├── database.js           # Conexión a PostgreSQL con Sequelize
│   │   ├── jwt.js                # Configuración de JWT
│   │   └── email.js              # Configuración de email
│   │
│   ├── models/                   # Modelos de Sequelize (tablas)
│   │   ├── User.js               # Modelo de Usuario
│   │   ├── Transaction.js        # Modelo de Transacción
│   │   ├── Category.js           # Modelo de Categoría
│   │   ├── Budget.js             # Modelo de Presupuesto
│   │   └── index.js              # Exportación de modelos
│   │
│   ├── controllers/              # Lógica de negocio
│   │   ├── authController.js     # Login, registro, logout
│   │   ├── transactionController.js  # CRUD de transacciones
│   │   ├── categoryController.js     # CRUD de categorías
│   │   ├── budgetController.js       # CRUD de presupuestos
│   │   ├── statsController.js        # Estadísticas y reportes
│   │   └── profileController.js      # Perfil de usuario
│   │
│   ├── routes/                   # Definición de rutas
│   │   ├── auth.routes.js        # Rutas de autenticación
│   │   ├── transaction.routes.js # Rutas de transacciones
│   │   ├── category.routes.js    # Rutas de categorías
│   │   ├── budget.routes.js      # Rutas de presupuestos
│   │   ├── stats.routes.js       # Rutas de estadísticas
│   │   ├── profile.routes.js     # Rutas de perfil
│   │   └── index.js              # Registro de todas las rutas
│   │
│   ├── middlewares/              # Middlewares personalizados
│   │   ├── auth.middleware.js    # Verificar JWT token
│   │   ├── validate.middleware.js    # Validación de datos
│   │   ├── errorHandler.middleware.js # Manejo de errores
│   │   └── logger.middleware.js      # Logging personalizado
│   │
│   ├── validators/               # Esquemas de validación
│   │   ├── auth.validator.js     # Validaciones de auth
│   │   ├── transaction.validator.js  # Validaciones de transacciones
│   │   ├── budget.validator.js       # Validaciones de presupuestos
│   │   └── profile.validator.js      # Validaciones de perfil
│   │
│   ├── services/                 # Servicios auxiliares
│   │   ├── emailService.js       # Envío de emails
│   │   ├── tokenService.js       # Generación/validación de tokens
│   │   └── statsService.js       # Cálculos de estadísticas
│   │
│   ├── utils/                    # Utilidades y helpers
│   │   ├── helpers.js            # Funciones auxiliares
│   │   ├── constants.js          # Constantes de la app
│   │   └── errors.js             # Clases de errores personalizados
│   │
│   └── app.js                    # Configuración de Express
│
├── migrations/                   # Migraciones de base de datos
│   ├── 001-create-users.js
│   ├── 002-create-categories.js
│   ├── 003-create-transactions.js
│   └── ...
│
├── seeders/                      # Datos iniciales
│   └── default-categories.js    # Categorías predefinidas
│
├── tests/                        # Tests (futuro)
│   ├── unit/
│   └── integration/
│
├── .env                          # Variables de entorno (NO SUBIR A GIT)
├── .env.example                  # Plantilla de variables de entorno
├── .gitignore                    # Archivos ignorados por Git
├── package.json                  # Dependencias y scripts
├── package-lock.json             # Lock de versiones
├── server.js                     # Punto de entrada
└── README.md                     # Este archivo
```

---

## 📜 Scripts Disponibles

### Desarrollo

```bash
# Iniciar servidor con auto-reload (recomendado para desarrollo)
npm run dev

# Iniciar servidor normal
npm start
```

### Base de Datos (cuando esté configurado Sequelize)

```bash
# Ejecutar migraciones
npm run migrate

# Revertir última migración
npm run migrate:undo

# Ejecutar seeders (datos iniciales)
npm run seed

# Revertir seeders
npm run seed:undo
```

### Testing (futuro)

```bash
# Ejecutar tests
npm test

# Tests con coverage
npm run test:coverage
```

---

## 🔌 Endpoints de la API

**Base URL:** `http://localhost:3000/api`

### Autenticación

| Método | Endpoint | Descripción | Auth |
|--------|----------|-------------|------|
| POST | `/auth/register` | Registrar nuevo usuario | No |
| POST | `/auth/login` | Iniciar sesión | No |
| POST | `/auth/logout` | Cerrar sesión | Sí |
| POST | `/auth/forgot-password` | Solicitar código de recuperación | No |
| POST | `/auth/reset-password` | Cambiar contraseña con código | No |
| GET | `/auth/me` | Obtener datos del usuario actual | Sí |

### Transacciones

| Método | Endpoint | Descripción | Auth |
|--------|----------|-------------|------|
| GET | `/transactions` | Listar transacciones del usuario | Sí |
| GET | `/transactions/:id` | Obtener transacción específica | Sí |
| POST | `/transactions` | Crear nueva transacción | Sí |
| PUT | `/transactions/:id` | Actualizar transacción | Sí |
| DELETE | `/transactions/:id` | Eliminar transacción | Sí |

### Categorías

| Método | Endpoint | Descripción | Auth |
|--------|----------|-------------|------|
| GET | `/categories` | Listar todas las categorías | Sí |
| GET | `/categories/:id` | Obtener categoría específica | Sí |

### Presupuestos

| Método | Endpoint | Descripción | Auth |
|--------|----------|-------------|------|
| GET | `/budgets` | Listar presupuestos | Sí |
| GET | `/budgets/current` | Presupuestos del mes actual con estado | Sí |
| POST | `/budgets` | Crear presupuesto | Sí |
| PUT | `/budgets/:id` | Actualizar presupuesto | Sí |
| DELETE | `/budgets/:id` | Eliminar presupuesto | Sí |

### Estadísticas

| Método | Endpoint | Descripción | Auth |
|--------|----------|-------------|------|
| GET | `/stats/dashboard` | Dashboard principal | Sí |
| GET | `/stats/report` | Reporte por período | Sí |
| GET | `/stats/by-category` | Gastos por categoría | Sí |

### Perfil

| Método | Endpoint | Descripción | Auth |
|--------|----------|-------------|------|
| GET | `/profile` | Ver perfil | Sí |
| PUT | `/profile` | Actualizar perfil | Sí |
| PUT | `/profile/password` | Cambiar contraseña | Sí |
| DELETE | `/profile` | Eliminar cuenta | Sí |

**Nota:** Los endpoints marcados con "Auth: Sí" requieren el header:
```
Authorization: Bearer <token_jwt>
```

---

## 🗄️ Base de Datos

### Diagrama de Tablas

```
┌─────────────────────┐
│       users         │
├─────────────────────┤
│ PK  id              │
│     email           │
│     password_hash   │
│     name            │
│     created_at      │
│     updated_at      │
└──────────┬──────────┘
           │ 1
           │
           │ N
┌──────────┴──────────┐
│   transactions      │
├─────────────────────┤
│ PK  id              │
│ FK  user_id         │
│ FK  category_id     │
│     type            │
│     amount          │
│     description     │
│     notes           │
│     date            │
│     created_at      │
│     is_deleted      │
└─────────────────────┘

┌─────────────────────┐
│    categories       │
├─────────────────────┤
│ PK  id              │
│     name            │
│     type            │
│     icon            │
│     color           │
└─────────────────────┘

┌─────────────────────┐
│      budgets        │
├─────────────────────┤
│ PK  id              │
│ FK  user_id         │
│ FK  category_id     │
│     amount_limit    │
│     month           │
│     year            │
│     created_at      │
└─────────────────────┘
```

### Acceso a la Base de Datos

**Desde pgAdmin 4:**
1. Abrir pgAdmin 4
2. Conectarse a PostgreSQL 18
3. Navegar a: Servers → PostgreSQL 18 → Databases → gestor_gastos_db

**Desde línea de comandos:**
```bash
psql -U postgres -d gestor_gastos_db
```

### Comandos Útiles de PostgreSQL

```sql
-- Ver todas las tablas
\dt

-- Describir estructura de una tabla
\d nombre_tabla

-- Ver todos los usuarios
SELECT * FROM users;

-- Ver todas las transacciones
SELECT * FROM transactions;

-- Salir
\q
```

---

## 🎯 Próximos Pasos

### Sesión 2: Sequelize y Modelos

1. **Configurar Sequelize**
   - Instalar Sequelize CLI
   - Crear archivo de configuración
   - Probar conexión con la BD

2. **Crear Modelos**
   - Modelo User
   - Modelo Category
   - Modelo Transaction
   - Modelo Budget
   - Modelo PasswordReset

3. **Migraciones**
   - Crear migraciones para cada modelo
   - Ejecutar migraciones
   - Verificar tablas en pgAdmin

4. **Seeders**
   - Crear categorías por defecto
   - Ejecutar seeders

### Sesión 3: Autenticación

1. **Endpoints de Auth**
   - POST /api/auth/register
   - POST /api/auth/login
   - Middleware de autenticación JWT

2. **Testing**
   - Probar registro con Postman/Thunder Client
   - Probar login
   - Verificar token JWT

### Sesión 4-7: CRUD y Features

- Endpoints de transacciones
- Endpoints de presupuestos
- Endpoints de estadísticas
- Validaciones completas
- Manejo de errores robusto

### Sesión 8: Deploy

- Configurar Railway/Render
- Subir base de datos a la nube
- Deploy del backend
- Testing en producción

---

## 📊 Progreso de Desarrollo

### Fase 1: Setup y Fundamentos ✅
- [x] Inicializar proyecto Node.js
- [x] Configurar Express
- [x] Middlewares básicos
- [x] Estructura de carpetas
- [x] Variables de entorno
- [x] PostgreSQL instalado
- [x] Base de datos creada
- [x] Servidor funcionando
- [x] Repositorio en GitHub

### Fase 2: Sequelize y Modelos 🔄
- [ ] Configurar Sequelize
- [ ] Crear modelos (User, Transaction, Category, Budget)
- [ ] Migraciones
- [ ] Seeders de categorías
- [ ] Testing de conexión

### Fase 3: Autenticación 📋
- [ ] Endpoint de registro
- [ ] Endpoint de login
- [ ] Middleware JWT
- [ ] Hash de contraseñas
- [ ] Validaciones

### Fase 4: Transacciones 📋
- [ ] CRUD completo
- [ ] Filtros y búsqueda
- [ ] Paginación
- [ ] Validaciones

### Fase 5: Presupuestos 📋
- [ ] CRUD de presupuestos
- [ ] Cálculo de estado
- [ ] Alertas

### Fase 6: Estadísticas 📋
- [ ] Dashboard
- [ ] Reportes por período
- [ ] Gráficas de datos

### Fase 7: Deploy 📋
- [ ] Configurar producción
- [ ] Deploy backend
- [ ] Deploy base de datos
- [ ] Testing en producción

---

## 🐛 Troubleshooting

### El servidor no inicia

**Error:** `Error: listen EADDRINUSE: address already in use :::3000`

**Solución:** El puerto 3000 está ocupado.

```bash
# Windows - Matar proceso en puerto 3000
netstat -ano | findstr :3000
taskkill /PID <PID> /F

# Linux/Mac
lsof -ti:3000 | xargs kill -9
```

O cambia el puerto en `.env`:
```env
PORT=3001
```

---

### No se conecta a PostgreSQL

**Error:** `Connection refused` o `ECONNREFUSED`

**Soluciones:**

1. Verificar que PostgreSQL esté corriendo:
```bash
# Windows
Get-Service -Name postgresql-x64-18

# Linux/Mac
sudo systemctl status postgresql
```

2. Verificar credenciales en `.env`:
```env
DB_PASSWORD=tu_contraseña_correcta
```

3. Verificar que la base de datos exista:
```bash
psql -U postgres -l
```

---

### Error de autenticación PostgreSQL

**Error:** `password authentication failed for user "postgres"`

**Solución:** La contraseña en `.env` no es correcta. Verifica en pgAdmin cuál es la contraseña que funciona.

---

### Dependencias no se instalan

**Error:** `npm ERR! code ENOENT`

**Solución:**

```bash
# Limpiar cache de npm
npm cache clean --force

# Eliminar node_modules y package-lock.json
rm -rf node_modules package-lock.json

# Reinstalar
npm install
```

---

### Git push falla

**Error:** `! [rejected] main -> main (non-fast-forward)`

**Solución:**

```bash
# Opción 1: Pull primero
git pull origin main --allow-unrelated-histories
git push origin main

# Opción 2: Force push (¡CUIDADO! Solo si estás seguro)
git push origin main --force
```

---

## 📞 Información de Contacto

**Desarrollador:** Orlando Díaz  
**GitHub:** [github.com/Orlando-Diaz](https://github.com/Orlando-Diaz)  
**Repositorio Backend:** [gestor-gasto-backend](https://github.com/Orlando-Diaz/gestor-gasto-backend)  
**Repositorio Frontend:** [gestor-gastos-frontend](https://github.com/Orlando-Diaz/gestor-gastos-frontend)  

---

## 📄 Licencia

Este proyecto es privado y con fines educativos.

---

## 🙏 Agradecimientos

Proyecto desarrollado como parte del aprendizaje de desarrollo fullstack con Node.js, Express, PostgreSQL y React Native.

---

**Última actualización:** 14 de Mayo, 2026  
**Versión del documento:** 1.0.0# gestor-gastos-api
Backend API REST con Node.js + Express + PostgreSQL para app de gestión de gastos
