# Madrid Cultural Dashboard (100 días)

Un único `index.html` listo para publicar en **GitHub Pages** o **Netlify**. Carga datos en tiempo real desde `datos.madrid.es` con *fallback* automático (proxy CORS y CSV) y guarda un *snapshot* en `localStorage` para uso sin conexión temporal.

## Publicar

### Opción A — GitHub Pages
1. Crea un repo nuevo (p.ej. `madrid-dashboard`).
2. Sube `index.html` a la rama `main`.
3. Settings → Pages → Source: *Deploy from a branch* → `main` / root.
4. Abre la URL que te da GitHub Pages.

### Opción B — Netlify
1. Entra en app.netlify.com y pulsa **Add new site → Deploy manually**.
2. Arrastra `index.html` (o todo el ZIP) y listo.

> También sirve en local con `python -m http.server 8080` y luego abrir `http://localhost:8080`.

## Cómo funciona la conexión
- Intenta **JSON directo**: `https://datos.madrid.es/egob/catalogo/206974-0-agenda-eventos-culturales-100.json`
- Si hay CORS, usa **AllOrigins**. Si también falla, usa **r.jina.ai**.
- Si el JSON no está disponible, intenta el **CSV** equivalente.
- Si todo falla, usa el **snapshot** en `localStorage` (si existe y tiene menos de 6 h).

## Personalización rápida
- Cambia el TTL del snapshot: `SNAPSHOT_TTL_HOURS` en el `<script>`.
- Desactiva el autorefresco cambiando `setInterval(updateFromAPI, 3600000)`. 
- Los filtros disponibles: Distrito, Tipo, Precio, Fecha.

## Créditos
- Datos: Ayuntamiento de Madrid — Portal de Datos Abiertos.
- Mapas: OpenStreetMap + Leaflet.
- Gráficos: Chart.js.