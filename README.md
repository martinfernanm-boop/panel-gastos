# Mi Panel de Gastos

Panel personal de gastos (Chile, CLP) en **un solo archivo HTML**, gratis de punta a punta:

- 📬 Lee las notificaciones de cargo/transferencia del banco directo desde Gmail (OAuth de solo lectura).
- 🤖 Extrae monto, comercio, fecha y categoría con Gemini (free tier).
- 📊 Dashboard: total del mes, comparación con el anterior, promedio diario, proyección de fin de mes, donut por categoría y tendencia de 6 meses.
- 💡 Insights automáticos: top comercio, mayor gasto, categoría que más subió y gastos recurrentes detectados (🔁).
- 🗂 Tabla con búsqueda, filtros, orden, edición de categoría/nota y export CSV/JSON.
- 💬 Chat con IA que responde preguntas sobre tus gastos.
- 🌙 Modo claro/oscuro.
- 📄 Carga manual de cartolas (CSV o texto pegado).

**Demo/producción:** https://martinfernanm-boop.github.io/panel-gastos/

## Cómo usarlo

1. Abre la página (o sirve `index.html` con `python3 -m http.server 8000`).
2. Sigue [SETUP.md](SETUP.md) para crear tus credenciales gratis (~15 min, una vez).
3. Aprieta **Sincronizar ahora**.

Sin backend: los datos y credenciales viven solo en `localStorage` de tu navegador y las llamadas van directo a las APIs de Google.
