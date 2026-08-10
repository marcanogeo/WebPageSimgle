Landing Page — Astro + Vue + Tailwind CSS

Maquetación de landing page dividida en componentes reutilizables, lista para producción.

Estructura

src/
├── components/
│   ├── Header.vue          Navegación fija con menú móvil (isla Vue, client:load)
│   ├── Hero.astro          Sección principal con CTA (estático, sin JS)
│   ├── Services.astro      Grid de servicios generado desde un array de datos (estático)
│   ├── About.astro         Narrativa + valores del equipo (estático)
│   ├── ContactForm.vue     Formulario con estado de envío (isla Vue, client:visible)
│   └── Footer.astro        Pie de página con enlaces y redes (estático)
├── layouts/
│   └── Layout.astro        <head>, meta tags y estilos globales
├── pages/
│   └── index.astro         Ensambla todos los componentes
└── styles/
└── global.css          Fuentes, reset y utilidades base

Por qué solo dos componentes son Vue

Astro renderiza .astro como HTML estático por defecto (0 KB de JS). Solo Header y
ContactForm necesitan interactividad en el cliente (menú móvil, estado de envío), así
que son los únicos hidratados como islas Vue:

Header.vue usa client:load porque el menú debe responder desde el primer render.
ContactForm.vue usa client:visible porque puede esperar a que el usuario haga scroll
hasta el formulario antes de cargar su JS.

Si prefieres convertir Hero, Services, About o Footer a Vue también (por ejemplo,
para reutilizar lógica con otra app Vue), el patrón es el mismo: crea el .vue, impórtalo
en index.astro y añade la directiva client:* que corresponda según si necesita
interactividad inmediata (client:load), diferida (client:idle) o solo al hacerse
visible (client:visible).

Instalación

npm install
npm run dev

El sitio queda disponible en http://localhost:4321.

Build

npm run build
npm run preview

Formulario de contacto

ContactForm.vue admite dos proveedores mediante props, sin necesidad de backend propio.
El envío se hace por fetch para mostrar estados de "enviando / éxito / error" sin
recargar la página.

Opción A — Netlify Forms (por defecto)

Al desplegar en Netlify:

Sube el proyecto a un repositorio conectado a Netlify.
Netlify detecta el formulario en el HTML generado en build gracias al <form> oculto
(hidden) con data-netlify="true" que incluye el componente — es necesario porque
Netlify escanea el HTML estático del build, no ejecuta el JS de Vue para detectarlo.
Las respuestas aparecerán en Site settings → Forms dentro del panel de Netlify.

No cambies nada en index.astro; el uso por defecto ya es:

<ContactForm client:visible />

Opción B — Formspree

Crea un formulario en formspree.io y copia su ID
(la parte final de tu endpoint, ej. xandalzp en https://formspree.io/f/xandalzp).
En ../../../Downloads/landing-astro 2/src/pages/index.astro, sustituye:

<ContactForm client:visible provider="formspree" formspreeId="TU_ID_DE_FORMSPREE" />

El componente enviará automáticamente un POST con JSON a
https://formspree.io/f/TU_ID_DE_FORMSPREE.

Personalización rápida

Colores y tipografías: editar ../../../Downloads/landing-astro 2/tailwind.config.cjs (paleta teal/gold/cream/ink)
y la importación de Google Fonts en ../../../Downloads/landing-astro 2/src/styles/global.css.
Contenido de servicios: editar el array services al inicio de Services.astro.
Textos e imágenes del Hero: editar directamente Hero.astro.
Enlaces del footer: editar el array columns en Footer.astro.

Accesibilidad y buenas prácticas incluidas

HTML semántico (header, main, section, footer, nav).
Foco de teclado visible en enlaces, botones y campos de formulario.
Menú móvil con aria-expanded y aria-controls.
Honeypot anti-spam en el formulario de Netlify.
Respeta prefers-reduced-motion.
Enlace "Saltar al contenido" para navegación por teclado/lectores de pantalla.
