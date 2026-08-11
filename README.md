# Nexo Digital — Landing page

Landing page responsive para una empresa ficticia de servicios digitales. El proyecto documenta el proceso de convertir una propuesta creada con Figma Make en una implementación frontend propia, accesible y mantenible.

La referencia visual original fue generada con React, TypeScript y Tailwind CSS. Para la versión final se replanteó la arquitectura utilizando Astro para el contenido estático y Vue únicamente donde existe interacción.

## Objetivos del proyecto

- Traducir una propuesta visual de Figma Make a código estructurado y comprensible.
- Practicar maquetación responsive con un enfoque mobile first.
- Construir una landing rápida, semántica y con poco JavaScript en el navegador.
- Aplicar un sistema visual consistente mediante tokens de diseño.
- Mostrar en el portfolio tanto el resultado como las decisiones tomadas durante el desarrollo.

## Tecnologías

- **Astro 7:** estructura, composición de páginas y renderizado estático.
- **Vue 3:** estado e interacción del formulario de contacto.
- **Tailwind CSS 4:** estilos, responsive y tokens visuales.
- **TypeScript:** tipado de componentes y configuración estricta.
- **Vite:** integración de Tailwind y herramientas de desarrollo de Astro.

## Decisiones de arquitectura

La mayor parte de la landing no necesita JavaScript en el navegador. Por ese motivo, `Header`, `Hero`, `Services`, `About`, `WhyUs` y `Footer` son componentes Astro.

El formulario se implementa como una isla Vue y se hidrata solamente cuando está próximo a entrar en pantalla:

```astro
<ContactForm client:visible />
```

Esta separación permite conservar la interactividad necesaria sin convertir toda la página en una aplicación cliente.

## Sistema visual

La dirección visual reproduce la propuesta de Figma Make:

| Uso | Valor |
| --- | --- |
| Navy principal | `#0F172A` |
| Navy secundario | `#1E293B` |
| Azul de acción | `#1D4ED8` |
| Azul claro | `#3B82F6` |
| Dorado | `#F59E0B` |
| Dorado claro | `#FCD34D` |
| Tipografía de títulos | Fraunces |
| Tipografía de interfaz | Inter |

Los colores y las fuentes están centralizados en `src/styles/global.css` mediante `@theme`, evitando valores arbitrarios repartidos entre los componentes.

## Secciones

- Header fijo con navegación responsive.
- Hero dividido entre contenido y fotografía.
- Servicios presentados en tarjetas reutilizables.
- About con información, métricas e imagen.
- Beneficios de trabajar con Nexo Digital.
- Formulario de contacto interactivo.
- Footer con navegación secundaria.

## Estructura

```text
src/
├── components/
│   ├── About.astro
│   ├── ContactForm.vue
│   ├── Footer.astro
│   ├── Header.astro
│   ├── Hero.astro
│   ├── ServiceCard.astro
│   ├── Services.astro
│   └── WhyUs.astro
├── layouts/
│   └── Layout.astro
├── pages/
│   └── index.astro
└── styles/
    └── global.css
```

## Accesibilidad y responsive

El proyecto incluye:

- HTML semántico y jerarquía de encabezados.
- Enlace para saltar directamente al contenido principal.
- Etiquetas y atributos de autocompletado en el formulario.
- Estados del formulario anunciados mediante `role="status"` y `role="alert"`.
- Indicadores visibles de foco para navegación con teclado.
- Menú adaptado a pantallas pequeñas.
- Compatibilidad con `prefers-reduced-motion`.
- Imágenes con texto alternativo y dimensiones declaradas.
- Ausencia de desbordamiento horizontal en móvil.

## Instalación

Requiere Node.js `22.12.0` o superior.

```bash
npm install
npm run dev
```

Astro mostrará en la terminal la dirección local del servidor, normalmente `http://localhost:4321`.

## Comprobaciones

```bash
npm run build
npm run astro -- check
```

El primer comando genera la versión estática de producción. El segundo comprueba los componentes Astro, Vue y TypeScript.

## Estado del formulario

El formulario actual es una demostración de interfaz: valida los campos con HTML y simula los estados de envío, éxito y error. Todavía no transmite información a un servicio externo.

Antes de publicar el sitio será necesario conectarlo a un backend o proveedor de formularios, por ejemplo Formspree o Netlify Forms, y actualizar el texto de confirmación.

## Créditos

- Diseño de referencia creado con Figma Make.
- Fotografías procedentes de [Unsplash](https://unsplash.com/).

## Licencia

Este proyecto se distribuye bajo la **Licencia MIT**. Puedes estudiar, modificar y reutilizar el código, siempre que conserves el aviso de copyright y la licencia original.

---

Proyecto creado como ejercicio de diseño a código y como pieza de portfolio frontend.
