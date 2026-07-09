# Setup del Panel de Gastos

Guía única para dejar el panel funcionando (~15 min, todo gratis). Solo se hace una vez por navegador.

## 1. API key de Gemini (IA que lee los correos)

1. Entra a [aistudio.google.com/apikey](https://aistudio.google.com/apikey) con tu cuenta Gmail.
2. **Create API key** → copia la key (`AIza...`).
3. Pégala en el panel: botón **⚙️ Configurar** → campo 1.

Free tier: no requiere tarjeta. El panel usa `gemini-2.5-flash-lite` y cae automáticamente a otros modelos si está saturado.

## 2. Google OAuth Client ID (acceso de solo lectura a Gmail)

1. Entra a [console.cloud.google.com](https://console.cloud.google.com) → crea un proyecto (ej: `panel-gastos`).
2. **APIs & Services → Library** → busca **Gmail API** → **Enable**.
3. **APIs & Services → OAuth consent screen**:
   - User type: **External** → Create.
   - Rellena nombre de la app y tu correo. Guarda.
   - En **Test users** agrega tu propio Gmail.
4. **APIs & Services → Credentials → Create Credentials → OAuth client ID**:
   - Application type: **Web application**.
   - **Authorized JavaScript origins**:
     - `https://TU-USUARIO.github.io` (producción)
     - `http://localhost:8000` (desarrollo local, opcional)
   - Create → copia el **Client ID** (`...apps.googleusercontent.com`). El client secret no se usa.
5. Pégalo en el panel: **⚙️ Configurar** → campo 2 → **Conectar Gmail** → autoriza en el popup.

Notas:
- El scope es `gmail.readonly`: el panel solo lee, jamás escribe ni borra correos.
- En modo Testing el token dura 1 hora; el panel lo renueva solo. Si el navegador bloquea el popup de renovación, el panel te lo dirá — usa **Conectar Gmail** de nuevo.

## 3. Ajustes de sincronización

En **⚙️ Ajustes** de la tarjeta "Sincronizar correo":

- **Remitentes**: direcciones desde las que tu banco manda notificaciones (uno por línea). Ej Banco Edwards / Banco de Chile:
  - `enviodigital@bancoedwards.cl`
  - `serviciodetransferencias@bancochile.cl`
- **Keywords del asunto**: solo se procesan correos cuyo asunto contenga alguna. Ej: `Cargo, Transferencia a Terceros`. Los avisos de transferencias *recibidas* ("Aviso de transferencia") quedan fuera automáticamente por no calzar.
- **Ventana en días**: cuántos días hacia atrás buscar (máx. 180).

## 4. Dónde viven tus datos

Todo (gastos, credenciales, chat) queda en `localStorage` del navegador. Nada se sube a ningún servidor propio; las únicas llamadas salen de tu navegador directo a las APIs de Google.

- **Respaldo**: sección "Configuración y datos" → Exportar JSON (respaldo completo) o CSV (para Excel).
- Si limpias el navegador, importa el JSON y vuelve a pegar las credenciales.

## Problemas comunes

| Síntoma | Solución |
|---|---|
| "El navegador bloqueó el popup de Google" | Permite popups para el sitio y aprieta **Conectar Gmail** |
| "Gemini alcanzó su límite (429)" | Espera un minuto; el panel ya reintenta solo |
| No aparecen gastos nuevos | Revisa remitentes/keywords en ⚙️ Ajustes; para releer correos usa **↻ Re-procesar** |
| Cambios del repo no se ven | Hard reload: `Cmd+Shift+R` (GitHub Pages cachea) |
