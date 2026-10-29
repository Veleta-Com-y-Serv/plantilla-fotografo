# Plantilla «Fotografía y vídeo» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **oscuro**
(«hoja de contactos»: bandas a sangre, negro de cuarto oscuro, rótulos en mayúsculas pesadas, números de fotograma y
marcas de visor). Todo en castellano de España, frases cortas, sin jerga. El brief de diseño está en `DISEÑO.md`.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa; no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores`. `fondo` es el fondo general (oscuro), `texto` el texto y las bandas claras, `primario` las bandas de color (el estudio, contacto, cabecera del aviso legal) y `acento` los botones, la banda de la frase y los detalles. `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…). La tinta sobre el acento y el primario (blanca o negra) se calcula sola en `src/styles/global.css` (`--tinta-acento`, `--tinta-primario`): el diseño aguanta un tema claro.
- **Tipografías y aspecto general**: `src/styles/global.css` (variables `--fuente-titulos` «Arial Black»/sistema, `--fuente-serif` para frases, `--fuente-mono` para antetítulos y botones; clases `.banda-oscura`, `.banda-clara`, `.banda-primario`, `.banda-acento`, `.visor`, `.pelicula`, `.contorno`, botones `.btn`/`.btn-sec`, cabecera `.cabecera--visor` y pie `.pie--negativo`). Fuentes del sistema: no añadas fuentes externas.
- **Imágenes**: en `public/`. Las fotos del ejemplo van en `public/fotos/` (las genera la plataforma a partir de `fotos.json`); los SVG de respaldo con el mismo nombre en `public/placeholders/`. Personas: `/placeholders/persona.svg`.
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = inicial en un recuadro + nombre en mayúsculas.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie` (true en plan gratis).

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`, en el orden de `site.yaml`.
- `hero` → `hero.astro`: foto a sangre a pantalla completa con marcas de visor, nombre del negocio enorme, `titulo` en serif, `texto`, `cta` y `cta_secundario`. La cabecera es transparente sobre esta foto (si el hero es la primera sección y tiene imagen).
- `galeria` → `galeria.astro`: mosaico de borde a borde sin márgenes (2/3/4 columnas) que siempre cierra en rectángulo; `galeria` es una lista de rutas (1-24); `cta` opcional.
- `sesiones` → `sesiones.astro`: filas 50/50 en zigzag con la foto a sangre; lista `sesiones`.
- `sobre` → `sobre.astro`: banda primario 50/50 con foto, texto y `personas`; `declaracion` = banda de acento con la frase enorme.
- `proceso` → `proceso.astro`: pasos (`items` con `icono`) como fotogramas de una tira de película.
- `opiniones` → `opiniones.astro`: `testimonios` (texto, autor, nota); la primera, enorme.
- `cta` → `cta.astro`: banda con foto de fondo (o de acento sin foto), título enorme y dos botones.
- `preguntas` → `preguntas.astro`: acordeón `details/summary`; sin preguntas no se pinta.
- `contacto` → `contacto.astro`: datos + formulario `mailto` con «Qué necesitas» (los nombres de las sesiones) y fecha; `boton` opcional.
- `texto` → `texto.astro`: diseño genérico para apartados nuevos (`tipo: texto`).

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`. Mantén la alternancia de bandas (oscura, clara, color) si puedes: galería y proceso son oscuras, sesiones y opiniones claras, sobre y contacto de color.
3. **Cambiar textos, teléfonos, horarios, fotos, sesiones y precios**: solo en `site.yaml`. Si un texto contiene comas o «: » dentro de `{ … }`, ponlo entre comillas. Precios siempre como cadena (`"desde 120 €"`). `incluye` es una cadena con «;».
4. **Listas planas**: nunca una lista dentro de un elemento de lista; máximo 24 elementos.
5. **Página nueva**: crea `src/pages/<slug>.astro` con `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`; enlázala en `site.yaml → menu`. Ejemplo: `src/pages/aviso-legal.astro`.
6. **Sección nueva**: un id nuevo en `site.yaml` con `tipo: <diseño existente>` (por ejemplo `tipo: texto` o `tipo: sesiones`), o un componente nuevo en `src/components/secciones/<id>.astro` que use `seccion(id)`, una clase `.banda-*` a todo el ancho y `.contenedor` dentro. `src/pages/index.astro` la recoge sola.
7. **No tocar** `src/pages/index.astro`, `src/layouts/Base.astro` (salvo las variantes de cabecera y pie), `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio y de las preguntas, robots, sitemap y llms.txt), salen solos de `site.yaml`. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
8. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida), bandas a todo el ancho (nada de cajas centradas estrechas con tarjetas), 16 px de margen lateral del texto en móvil (`.contenedor`), botones de 44 px como mínimo, sin scroll horizontal a 375 px. `alt` sacado del contenido (`altHero`, `altFicha`, `altGaleria`, `altSeccion` de `src/lib/seo.ts`); las decorativas, `alt=""`.
9. El formulario no tiene servidor: abre el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro`.
10. En los textos de la web, nada de jerga técnica: «tu web», «tu galería», «tu sesión».

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.

## Campos propios de esta plantilla (además del esquema común)
- `sesiones.sesiones[]`: {nombre, texto, precio, duracion, incluye («;»), imagen, destacado}.
- `sobre.declaracion`: frase grande (banda de acento); `sobre.personas[]`: {nombre, cargo, foto}.
- `opiniones.testimonios[]`: {texto, autor, nota}.
- `cta`: banda de llamada a la acción con `imagen`, `cta` y `cta_secundario`.
- `contacto.boton`: texto del botón del formulario.
