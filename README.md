# Sitio web — Jolix Asesorías

Sitio estático de una sola página (`index.html`, sin dependencias de build). Incluye el brand kit (logo, paleta, tipografía Poppins/Work Sans) y las secciones Servicios, Precios, Quiénes Somos y Contacto.

## Publicar en GitHub Pages con el dominio jolixasesorias.com

1. **Crea un repositorio en GitHub** (público, para Pages gratis) y sube este contenido:

   ```bash
   git remote add origin https://github.com/<tu-usuario>/<tu-repo>.git
   git branch -M main
   git push -u origin main
   ```

2. **Activa GitHub Pages**: en el repo, ve a *Settings → Pages* → *Source: Deploy from a branch* → rama `main`, carpeta `/ (root)` → Save.

3. **Conecta tu dominio jolixasesorias.com**:
   - En *Settings → Pages → Custom domain*, escribe `jolixasesorias.com` y guarda (esto ya está preconfigurado en el archivo `CNAME` de este repo).
   - En el panel DNS donde administras el dominio (Google Domains / Squarespace Domains / Google Workspace), agrega:

     | Tipo  | Nombre | Valor                  |
     |-------|--------|------------------------|
     | A     | @      | 185.199.108.153        |
     | A     | @      | 185.199.109.153        |
     | A     | @      | 185.199.110.153        |
     | A     | @      | 185.199.111.153        |
     | CNAME | www    | `<tu-usuario>.github.io` |

   - Espera la propagación DNS (minutos a algunas horas) y marca "Enforce HTTPS" en GitHub Pages una vez verificado.

## Alternativas más simples (sin tocar registros A manualmente)

Si prefieres evitar los registros DNS manuales, se puede importar este mismo repositorio en **Vercel**, **Netlify** o **Cloudflare Pages** — los tres tienen plan gratuito, detectan que es HTML estático sin configuración adicional, y guían paso a paso para conectar `jolixasesorias.com` desde su propio panel.

## Formulario de contacto (Web3Forms + hCaptcha)

El formulario de la sección Contacto envía a **Web3Forms** (access key ya incrustada en `index.html`) y protege el envío con **hCaptcha** real (widget cargado desde `web3forms.com/client/script.js`).

**Un paso pendiente en tu panel de Web3Forms** antes de que el captcha se aplique de verdad:
1. Entra a tu dashboard en [web3forms.com](https://web3forms.com)
2. Abre el formulario "Contacto" → Settings
3. Activa la opción **hCaptcha** (usa la site key pública compartida de Web3Forms; no necesitas crear cuenta en hcaptcha.com para el plan gratis)

Sin ese paso, el widget visual igual aparece, pero Web3Forms no exige el token en el servidor.

Nota: este formulario **no funciona dentro de un Artifact de Claude** (la política de seguridad de esa vista bloquea peticiones de red salientes a servicios externos) — solo funciona una vez publicado en un hosting real como GitHub Pages.

## Editar contenido

Todo el sitio vive en `index.html` (HTML + CSS + un script pequeño para el menú móvil). Los colores y tipografía están centralizados como variables CSS al inicio del archivo (`:root`), incluyendo el modo oscuro automático.
