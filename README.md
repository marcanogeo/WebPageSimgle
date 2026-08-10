WebPageSimple — Landing con Astro + Vue + Tailwind


Proyecto de landing page creado con Astro, Vue (islas) y Tailwind CSS. Lista para editar y desplegar, contiene componentes estáticos (.astro) y componentes hidratados (Vue) donde hace falta interactividad.

Puntos importantes sobre hidratación

La mayoría de las piezas usan .astro y se renderizan estáticamente para minimizar JS. El formulario de contacto (ContactForm.vue) es una isla Vue y se instancia en index.astro con client:visible.

Correcciones respecto al README anterior

- Header se proporciona como Header.astro (no Header.vue). El README original referenciaba Header.vue por error.
- ContactForm.vue es actualmente una demo que simula el envío (delay local). No incluye props para proveedores (Netlify/Formspree) ni lógica de envío a terceros. Si quieres soporte para Netlify/Formspree, hay que añadir los props y adaptar la plantilla del <form> en src/components/ContactForm.vue.
- No se han encontrado archivos tailwind.config.* en el repo. Si Tailwind no está configurado, ejecutar "npx tailwindcss init -p" y añadir la configuración recomendada en astro.config.
- Se eliminaron rutas incorrectas que apuntaban a carpetas en Downloads.

Instalación y desarrollo

Requisitos: Node.js >= 22.12.0 (según package.json).

npm install
npm run dev

Por defecto Astro sirve en http://localhost:4321.

Build y preview

npm run build
npm run preview

Formularios y despliegue

Actualmente ContactForm.vue muestra el estado de envío localmente y limpia campos tras una simulación. Para integrar con Netlify:
- Añadir un <form> con data-netlify="true" y los campos necesarios dentro de ContactForm.vue (o incluir un <form hidden> en el HTML generado) para que Netlify detecte el formulario en el build.

Para Formspree u otros proveedores:
- Añadir props (provider, formId) a ContactForm.vue y hacer fetch al endpoint del proveedor desde la función submitForm.

Sugerencia rápida para habilitar Netlify (ejemplo mínimo):
- Añadir attribute data-netlify="true" al <form> y un input name="form-name" value="contact" oculto. Luego desplegar en Netlify.

