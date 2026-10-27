# Mus de la Plaza

Juego de mus para cuatro personas, con salas mediante código/enlace y variantes de 4 u 8 reyes. Está construido con React, TypeScript y Vite; Vercel sirve la aplicación y Supabase proporciona las salas online.

## Preparar multijugador

1. Crea un proyecto en [Supabase](https://supabase.com/).
2. En **SQL Editor**, ejecuta el contenido de `supabase/schema.sql`.
3. En los ajustes de Realtime, deja habilitados Broadcast y Presence.
4. En la configuración de la app, copia la **Project URL** y la clave pública **anon/publishable**. No uses `service_role`.

## Subir el código a GitHub

Puedes hacerlo con GitHub Desktop:

1. Instala y abre GitHub Desktop e inicia sesión en GitHub.
2. Elige **File → Add local repository** y selecciona la carpeta `mus-online`.
3. Si GitHub Desktop indica que aún no es un repositorio, elige **create a repository** en esa carpeta.
4. Confirma los archivos y pulsa **Publish repository**. Puedes dejarlo privado o hacerlo público.

También puedes crear un repositorio vacío en GitHub y subir desde la página web los archivos de esta carpeta. No subas `.env.local`, `.env` ni claves privadas. La carpeta `node_modules` y `dist` se excluyen con `.gitignore`.

## Desplegar en Vercel

1. Entra en [Vercel](https://vercel.com/) e importa el repositorio de GitHub.
2. Vercel detectará Vite. Usa estos valores si solicita configuración:
   - **Build command:** `pnpm build`
   - **Output directory:** `dist`
   - **Install command:** `pnpm install --frozen-lockfile`
3. En **Environment Variables**, añade:
   - `VITE_SUPABASE_URL` = Project URL de Supabase
   - `VITE_SUPABASE_ANON_KEY` = clave pública anon/publishable
4. Pulsa **Deploy**. Vercel volverá a desplegar cada vez que subas cambios a GitHub.

`vercel.json` ya incluye la configuración de compilación y las rutas de la app.

## Desarrollo local

Necesitas Node.js 20 o superior y pnpm. En una terminal, desde esta carpeta:

```bash
pnpm install
pnpm dev
```

Puedes copiar `.env.example` a `.env.local` para probar la conexión online en local.

## Alcance y seguridad

El esquema SQL es una configuración de demostración con permisos abiertos para facilitar el prototipo. Úsalo con gente de confianza; no es adecuado para partidas públicas o competitivas. Para abrirlo al público, hay que proteger la creación/actualización de salas y validar los turnos en el servidor.
