# Son-risas

Landing page de una clínica dental ficticia. Está desplegada en Vercel y
versionada en `github.com/LuisMCGutierrez/son-risas` (privado).

## Cómo está hecho

Todo el sitio es **un único archivo**, `Son-risas/index.html`: HTML, CSS y JS
en línea, sin build, sin dependencias, sin assets externos salvo las fuentes de
Google. Esa restricción es deliberada, no una etapa provisional.

    Son-risas/index.html    el sitio entero
    Son-risas/README.md     el sistema de marca y los pasos para publicarlo
    Son-risas/vercel.json   cabeceras de seguridad y noindex
    .claude/launch.json     servidor local para previsualizar

**No introducir** un framework, un bundler, `package.json`, TypeScript ni
archivos CSS o JS separados. Si algo parece necesitarlo, plantearlo antes de
hacerlo.

## El sitio está en modo demostración

Los dentistas, cédulas, precios, domicilio y teléfonos son inventados, el
formulario no envía nada a ningún servidor y la página lleva `noindex` tanto en
el `<head>` como en las cabeceras de `vercel.json`.

Mientras eso siga así, **no se tocan sin que el usuario lo pida**:

- la franja `.demo`, el bloque `.demo-legal` y la línea de copyright
- `noindex` en el `<meta>` y `X-Robots-Tag` en `vercel.json`
- `demo: true` dentro de `const CLINICA`
- los datos ficticios

El README lleva la lista completa de los seis pasos para convertirlo en un
sitio real. Son decisión del usuario, no tareas pendientes.

## El sistema de marca

`Son-risas/README.md` documenta la regla con la que se hizo la página —*la
recta es la norma, la curva es la excepción*— los cuatro puntos donde algo se
curva y los cuatro tiempos del copy. Leerlo antes de tocar el CSS del guion o
de escribir copy nuevo: describe lo que hay hoy y por qué.

**En este proyecto, el skill `frontend-design` tiene prioridad sobre esas
reglas.** Cuando su criterio y el README no coincidan, manda el skill: el
README pasa de ser una restricción a ser el punto de partida del que se puede
salir. Esta prioridad es solo de aquí — vive en este archivo, no en el skill.

Lo que no cambia: al alterar una regla de marca hay que actualizar el README en
el mismo commit, para que siga describiendo la página que de verdad existe.

## Previsualizar y desplegar

El navegador integrado no abre `file://`, así que la vista previa va por
`preview_start` con la configuración `son-risas` de `.claude/launch.json`.

Desplegar, desde `Son-risas/`:

    npx vercel --prod

El plan Hobby es gratuito pero **solo para uso no comercial**.

## Git

`main` sigue a `origin/main`. `.gitattributes` fija finales de línea LF: el
sitio se sirve desde Linux y lo desplegado debe coincidir byte a byte con lo
versionado.

`.vercel/` está en `.gitignore` y **no debe entrar al repositorio**: contiene
los identificadores de la cuenta y del proyecto.
