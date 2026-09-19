# Son-risas — landing page

Maqueta de landing page para una clínica dental. Un solo archivo HTML, sin build
ni dependencias: se despliega como sitio estático.

## Desplegar en Vercel

    npx vercel          # despliegue de prueba, URL temporal
    npx vercel --prod   # despliegue definitivo

La primera vez pide iniciar sesión y confirmar la configuración del proyecto.
Acepta los valores por defecto: Vercel detecta el sitio estático solo.

## El sistema de marca

> **Precedencia:** en este proyecto el skill `frontend-design` manda sobre las
> reglas de este README cuando no coincidan (ver `CLAUDE.md`). Lo que sigue
> describe la página que existe hoy y el motivo de cada decisión; es el punto
> de partida, no una restricción.

«Son-risas» se lee de dos maneras, y la página apuesta por la segunda: reír
obliga a abrir la boca. Quien se avergüenza de sus dientes se ríe con la mano
encima, o no se ríe. La promesa no es «dientes bonitos», es una risa sin mano
encima.

**Eso no se dice en ninguna parte, y no debe decirse.** Se manifiesta de dos
formas, y las dos tienen reglas.

### La forma: una regla, cinco excepciones

> **La recta es la norma. La curva es la excepción y solo aparece donde algo
> se abre.**

El guion de la marca no es un carácter: es una caja con `border-bottom` y
altura fija. Al aplicarle el radio `var(--arco)` la recta se convierte en
sonrisa. Como la altura no cambia, nada empuja al texto de al lado.

Solo se curvan cinco cosas, cada una por un motivo:

| Dónde | Cuándo |
|---|---|
| Arco del hero | Se traza solo al cargar, una vez: la regla a tamaño completo |
| Wordmark del header | `:hover` / `:focus-visible` — la marca se abre al tocarla |
| Marcador del FAQ | Al desplegar la pregunta: abrir la pregunta es abrir la boca |
| Arco de la sección de cierre | Siempre |
| Favicon | Siempre |

Siguen rectos, y deben seguirlo, los filetes de sección, los puntos guía de
los precios y los bordes de los campos del formulario. **Si se curva todo,
deja de significar algo.**

El arco del hero es el único movimiento de la página: un trazo que se dibuja
una vez al llegar y no se vuelve a mover. `prefers-reduced-motion` lo deja ya
dibujado, nunca invisible. No añadir más animación en ninguna parte.

La profundidad del arco está ajustada a ojo, no por fórmula: la parte útil es
`alto − grosor del borde`, y por debajo del ~10% del ancho se lee recta,
por encima del ~35% se lee cuenco en vez de sonrisa. Al cambiar el tamaño de
un guion hay que reajustar su altura.

### El color y la letra: un impreso, no un consultorio

La página no se ve como una clínica: se ve como el presupuesto que te llevas
de la clínica. Esa es la promesa concreta de la marca («el presupuesto te lo
llevas contigo»), y es lo que gobierna color y tipografía.

| Token | Luz | Para qué |
|---|---|---|
| `--paper` | `#E9E0CC` | Fondo. Arena de tono medio, ni crema ni casi-blanco |
| `--paper-2` | `#DFD4BA` | Bandas, campos del formulario, pie |
| `--ink` | `#1B2036` | Tinta. Azul muy oscuro, cromático: nunca negro tintado |
| `--ink-2` | `#4F556B` | Texto secundario. Mínimo 4.5:1 sobre `--paper-2` |
| `--anil` | `#2743B8` | **El único acento.** No añadir un segundo color |

`--anil` es el azul de talavera. Al ajustar cualquiera de los dos tonos de
fondo hay que volver a medir `--ink-2` contra ambos: es el que va justo.

Dos familias, invertidas a propósito respecto de lo habitual:

- **Bricolage Grotesque** para titulares, botones, cifras y etiquetas. Una
  grotesca de display, no una serif de alto contraste.
- **Newsreader** para el texto corrido, con más interlineado del que llevaría
  una sans, porque es serif.

Las cifras van siempre en `font-variant-numeric:tabular-nums`: precios,
teléfonos, duraciones y cédulas alinean en columna.

**Nada de versalitas trackeadas como etiqueta sobre los encabezados**, ni
puntos medios separando datos («A · B · C»), ni una sola palabra del titular
en itálica o en color. Son los tics que la página quitó a propósito; el único
sitio donde sobreviven las versalitas es el aviso legal de maqueta, porque ahí
es un aviso y debe parecerlo.

Los precios se listan con puntos guía de impreso. El punto guía no decora:
dice que eso es una lista de costos de verdad, que es justo lo que promete la
sección. Por eso no se usa en ninguna otra lista.

### El texto: cuatro tiempos y ni uno más

«Risa», «ríe» y «sonríe» **no aparecen nunca** como eslogan ni en imperativo.
El tema entra siempre por acciones físicas, y cada pieza aparece una sola vez:

1. **Hero** — «La primera vez que abres la boca aquí, es para hablar.»
2. **FAQ, miedo al dentista** — «paramos cuando levantes la mano» (la mano como
   control del paciente, no como escondite)
3. **FAQ, las fotos** — «Llevo años tapándome la boca en las fotos», dicho por
   el paciente y no por la clínica
4. **Cierre** — «Aquí nadie se ha reído con la mano en la boca.»

Al añadir copy nuevo, no sumar un quinto tiempo. Si algo se nota, se quita una
pieza; no se añade otra.

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
