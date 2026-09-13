# Hyperion Roleplay — Bot de Discord para Roleplay

Bot de Discord todo-en-uno para servidores de roleplay. Gestión completa de servidores con panel de administración web, sistema de economía, whitelist, apertura/cierre de servidor, menú policial y más.

## 📋 Changelog v1.0.2

### ✨ Nuevas Funciones
- **Dashboard rediseñada** — estilo dark glass morphism, sidebar macOS, 8 páginas de configuración
- **Audit Logs** — registro completo de cambios (quién, qué, cuándo, antes → después)
- **Carrusel de imágenes** en la landing page con rotación cada 10s
- **Testimonials marquee** — reviews de usuarios con scroll infinito
- **URL routing** — `/dashboard/{guildId}` al configurar un servidor
- **Botón "Actualizar"** en General para re-fetchear configuración
- **Apertura side panels** — layout de 2 columnas con tabs (Cerrado | Votación | Abierto)
- **Profile dropdown** — avatar + cerrar sesión + cambiar cuenta
- **Guild switcher** — cambiar de servidor desde el sidebar
- **URL Recovery** — restaura el servidor seleccionado al refrescar
- **Error page OAuth** — página HTML estilizada en vez de JSON crudo
- **Auto-crear guild** — si el servidor no existe en la DB, se crea automáticamente
- **Nitro Rocket Fuel nameplate** en íconos de servidor

### 🐛 Correcciones
- XSS — función `esc()` aplicada a ~50 interpolaciones en innerHTML
- Entorno — campo `entornoChannel` corregido a `channel`
- Guild icon 404 — fallback a iniciales cuando el ícono no existe
- Audit logs 500 — retorna datos vacíos si la tabla no existe
- OAuth callback — redirige a página HTML en vez de JSON `{"error":"No code provided"}`
- Page refresh — `/dashboard/{guildId}` ahora sirve `app.html` en vez de 404
- Botones shimmer estilo Novix UI
- Server cards glass gradiente dark estilo iPhone Pro Max
- Profile dropdown cierra al hacer click fuera
- Syntax error en select dropdown (`});` faltante)
- 400 Bad Request — token expirado muestra toast y redirige

### 🔧 Mejoras Técnicas
- Prisma `AuditLog` model con índices para consultas rápidas
- API audit helper `createAuditLog()` y `diffAndAudit()`
- Todos los PUT routes instrumentados para capturar cambios
- GET `/guilds/:guildId/audit-logs` con paginación
- CSS variables: `--bg:#0a0a0c`, `--accent:#4f8ff7`, `--sidebar-w:280px`
- Premium removido del FREE (vive en MongoDB)

## 🛠️ Stack
- **Runtime:** Node.js 24+
- **Package Manager:** pnpm workspaces
- **Bot:** discord.js 14.x, TypeScript ESM/NodeNext
- **API:** Express 5, JWT, OAuth2
- **Database:** Prisma + PostgreSQL
- **Cache:** Redis (ioredis)
- **Dashboard:** HTML + JS vanilla, CSS glass morphism
- **Deploy:** Railway

## 🚀 Instalación

```bash
# Clonar el repositorio
git clone https://github.com/AchitoRD/hyperion-roleplay.git
cd hyperion-roleplay

# Instalar dependencias
pnpm install

# Configurar variables de entorno
cp .env.example .env
# Editar .env con tus credenciales

# Generar Prisma client
pnpm --filter @hyperion/database exec prisma generate

# Ejecutar migraciones
pnpm --filter @hyperion/database exec prisma migrate deploy

# Desarrollo
pnpm dev

# Build
pnpm build
```

## 📁 Estructura

```
hyperion/
├── apps/
│   ├── bot/          # Bot de Discord (discord.js 14)
│   ├── api/          # API REST (Express 5)
│   └── dashboard/    # Panel de administración web
├── packages/
│   ├── database/     # Prisma schema y migraciones
│   ├── shared/       # Funciones compartidas
│   └── logger/       # Logging (Pino)
└── dashboard/        # Archivos estáticos del dashboard
    ├── index.html    # Landing page
    ├── app.html      # Panel principal
    ├── app.js        # Lógica del dashboard
    └── assets/       # Imágenes y recursos
```

## 📄 Licencia

© 2026 Hyperion Studio. Todos los derechos reservados.
