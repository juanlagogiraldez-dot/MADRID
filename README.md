# Madrid Cultural Dashboard (GitHub Pages, sin CORS)

Este paquete publica `index.html` y usa un **GitHub Action** para descargar `latest.json` y `latest.csv` cada hora.
La web lee **solo `latest.json` del propio repo** → mismo origen → sin CORS.

## Pasos
1. Sube todo este paquete a tu repo (raíz), incluida la carpeta `.github/workflows/`.
2. Activa **Settings → Pages → Source: Deploy from a branch → Branch: main → /(root)**.
3. Abre `https://OWNER.github.io/REPO/`.
4. En **Actions**, ejecuta **Fetch Madrid Data** manualmente (Run workflow) para tener `latest.json` la primera vez.

> Nota: el cron es **UTC**. Si quieres cada 30 min, usa: `*/30 * * * *`.

## Cómo funciona
- El workflow guarda `latest.json`/`latest.csv` en la raíz del repo.
- `index.html` hace `fetch('latest.json?v=timestamp')` para evitar caché.
- Si falla, usa un snapshot en `localStorage` (si existe).

## Personaliza
- Cambia la frecuencia en `.github/workflows/fetch_dataset.yml`.
- Ajusta estilos/colores en el `<style>` de `index.html`.