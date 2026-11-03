# Plantilla NoExpertise · Fotografía y vídeo

Web oscura para fotógrafos y productoras de vídeo, con galería a borde completo y sesiones con precio.

- Sectores: fotografia, fotografo, video, productora, estudio-fotografico. Estilo: oscuro. Plan mínimo: gratis.
- Secciones: hero, galeria, sesiones, sobre, proceso, opiniones, cta, preguntas, contacto (y `texto` para apartados nuevos).
- Todo a ancho completo: bandas de borde a borde que alternan negro, claro, color y acento; hero a pantalla completa
  con foto a sangre; mosaico de galería sin márgenes que cierra siempre en rectángulo; sesiones en zigzag 50/50 con la
  foto tocando el borde. Móvil primero, sin scroll horizontal a 375 px.
- Ejemplo: Nordés Estudio, estudio ficticio de fotografía y vídeo en Gijón.
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio y de las preguntas frecuentes,
- Varias páginas (opcional, `paginas:` en la raíz de `site.yaml`): Inicio + una página por entrada (`{ ruta, titulo, secciones: "a; b" }`, hasta 6) con el menú hecho solo; reparto recomendado en `template.yaml → paginas`. Sin la clave, una sola página larga.
  `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Contenido editable en `site.yaml`; metadatos y guion del asistente en `template.yaml`; fotos a generar en
  `fotos.json`; reglas para el agente en `CLAUDE.md`; brief de diseño en `DISEÑO.md`.

## Campos propios

| Sección | Campo | Forma |
|---|---|---|
| `galeria` | `galeria` | lista de rutas de fotos (1-24) |
| `sesiones` | `sesiones` | `[{nombre, texto, precio, duracion, incluye, imagen, destacado}]`, `incluye` con «;» |
| `sobre` | `declaracion`, `personas` | frase grande; `[{nombre, cargo, foto}]` |
| `opiniones` | `testimonios` | `[{texto, autor, nota}]` |
| `cta` | `imagen`, `cta`, `cta_secundario` | banda de llamada a la acción |
| `contacto` | `boton` | texto del botón del formulario |

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`).
Imágenes de relleno (`public/placeholders/`) generadas para esta plantilla, sin licencias de terceros.

## Páginas propias
- Cada elemento de `secciones.sesiones.sesiones` con `detalle` tiene su página en `/sesiones/<slug>/` (`src/pages/[coleccion]/[slug].astro`).
- Campos opcionales de los elementos con ficha: `detalle` (párrafos separados por una línea en blanco), `slug` e `imagenes` («/fotos/a.jpg; /fotos/b.jpg»).
