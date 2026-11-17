# TBD — RPG Cooperativo Web (3 Jugadores)

Juego de rol de fantasía por navegador para hasta **3 jugadores** (estilo D&D simplificado) pensado para funcionar sin instalaciones en portátiles y Chromebooks, con respaldo por *HTTP long-polling* si los WebSockets están bloqueados.

> **Cambiar el título del juego**: edita la constante `GAME_TITLE` en `shared/src/constants.ts`.

---

## Ejecución local

1. Instala las dependencias:
   ```bash
   npm install
   ```
2. Crea un archivo `.env` en la raíz a partir de `.env.example`:
   ```env
   PORT=3001
   GEMINI_API_KEY=tu_clave_de_gemini_aqui
   ```
   *(Si no pones `GEMINI_API_KEY`, el juego usará automáticamente los 36 eventos locales de `server/src/events.json` sin bloquearse).*
3. Inicia el servidor y el cliente en desarrollo:
   ```bash
   npm run dev
   ```
4. Abre `http://localhost:5173` en 1 a 3 pestañas del navegador.

---

## Despliegue gratuito en Render (con WebSockets)

El proyecto está preparado para desplegarse como **un único servicio Web en Render** (el servidor Node/Express sirve el cliente compilado `client/dist` y gestiona Socket.io).

### Pasos para publicar en Render

1. **Sube este proyecto a un repositorio de GitHub** (público o privado).
2. Entra en [Render](https://render.com) y haz clic en **New + → Blueprint** (detectará `render.yaml` automáticamente) o **New + → Web Service** y selecciona tu repositorio.
3. Verifica la configuración:
   - **Runtime**: `Node`
   - **Plan**: `Free`
   - **Build Command**: `npm install && npm run build`
   - **Start Command**: `npm start`
   - **Health Check Path**: `/health`
4. En **Environment Variables**, añade:
   - `GEMINI_API_KEY` = tu clave gratuita de [Google AI Studio](https://aistudio.google.com/)
   - *(Opcional)* `GEMINI_MODEL` = `gemini-2.5-flash`
5. Haz clic en **Deploy**. Cuando termine, comparte el enlace `https://tu-app.onrender.com` con tus amigos para jugar.

> **Nota sobre el plan gratuito de Render**: tras 15 minutos sin actividad, el servicio entra en reposo y tarda ~30 segundos en despertar al abrir la URL. Los archivos locales (`server/data/rooms.json`) se reinician cuando Render reconstruye o duerme el contenedor en el plan gratuito.
