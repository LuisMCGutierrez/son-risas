# Son-risas — landing page

Maqueta de landing page para una clínica dental. Un solo archivo HTML, sin build
ni dependencias: se despliega como sitio estático.

## Desplegar en Vercel

    npx vercel          # despliegue de prueba, URL temporal
    npx vercel --prod   # despliegue definitivo

La primera vez pide iniciar sesión y confirmar la configuración del proyecto.
Acepta los valores por defecto: Vercel detecta el sitio estático solo.

## Antes de publicarlo como sitio real

El sitio está en **modo demostración**. Todo el contenido es ficticio.
Para convertirlo en el sitio real de una clínica hay que:

1. En `index.html`, bloque `const CLINICA`: poner el WhatsApp, teléfono y
   correo reales, y cambiar `demo: true` a `demo: false`.
   Mientras `demo` sea `true` el formulario no abre WhatsApp y los teléfonos
   no marcan, a propósito.
2. Sustituir nombres de los dentistas y **cédulas profesionales reales**
   (obligatorias en publicidad de servicios de salud en México).
3. Revisar precios, horarios y domicilio.
4. Quitar la franja `<div class="demo">` y el bloque `<div class="demo-legal">`.
5. Quitar `<meta name="robots" content="noindex...">` del `<head>` y el header
   `X-Robots-Tag` de `vercel.json`, para que Google pueda indexar el sitio.
6. Descomentar `canonical` y `og:url` en el `<head>` con el dominio definitivo.

## Nota sobre el plan de Vercel

El plan Hobby es gratuito pero solo para uso **no comercial**. El sitio de una
clínica que factura requiere plan Pro.
