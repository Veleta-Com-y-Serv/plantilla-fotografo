# Fotografía y vídeo: brief de diseño

Plantilla `fotografo` creada el 29/10/2026 a partir de `portfolio` con `php artisan plantillas:nueva` y rediseñada
entera (tanda «ancho completo»). Este fichero se queda en el repo: es lo que lee quien (persona o agente) rediseñe
la plantilla.

## Brief

- **Para quién**: fotógrafos de retrato, familia y boda, estudios fotográficos, videógrafos y pequeñas productoras
  (`fotografia, fotografo, video, productora, estudio-fotografico`). Su cliente entra a ver si le gusta el trabajo
  (galería), cuánto cuesta (sesiones) y si hay fecha (contacto).
- **Qué tiene que conseguir la web**: que pidan fecha o presupuesto (formulario con tipo de sesión y fecha, WhatsApp).
- **Tono y estilo** (`oscuro`): cinematográfico, rotundo, cercano. Sí: una hoja de contactos, el visor de una cámara,
  la luz de seguridad de un cuarto oscuro. No: la caja centrada estrecha con tarjetas blancas ni el minimalismo gris
  de `portfolio`.
- **Concepto «hoja de contactos»**: cada sección es una banda de borde a borde; el ritmo alterna negro (galería,
  proceso, preguntas), claro «papel» (sesiones, opiniones), color (sobre, contacto) y acento (la frase); números de
  fotograma (01, 02…) en monoespaciada o en contorno enorme, marcas de visor en las esquinas de las fotos,
  perforaciones de película como separadores.
- **Paleta de ejemplo**: fondo `#0c0c0d` (negro de cuarto oscuro), texto `#f1ede6` (papel hueso), primario `#123039`
  (azul petróleo del Cantábrico de noche), acento `#ff5a1f` (luz de seguridad naranja). Aguanta los cuatro del cliente:
  las bandas claras son `texto` sobre `fondo` invertidos, los derivados van con `color-mix` y la tinta sobre acento y
  primario se calcula con color relativo `oklch(from …)` (blanca si el color es oscuro, negra si es claro; respaldo fijo).
- **Tipografía** (sistema, sin descargas): títulos en «Arial Black»/system-ui 900 en mayúsculas con interletrado
  negativo; frases y precios en serif cursiva de sistema (Palatino/Georgia); antetítulos, botones, etiquetas y números
  en monoespaciada en mayúsculas espaciadas; texto en system-ui.
- **Apartados** en orden:
  1. `hero`: foto a sangre a pantalla completa (`min-h-[100svh]`), velo degradado, marcas de visor, nombre del negocio
     enorme (3,25 rem en móvil, 11 rem en escritorio), título en serif, párrafo corto y dos botones. Cabecera fija
     transparente encima que se vuelve sólida al bajar.
  2. `galeria`: mosaico de borde a borde sin márgenes; 2 columnas en móvil, 3 en tableta, 4 en escritorio; los tamaños
     (2×2, altas, anchas) se reparten por grupos para cerrar siempre en rectángulo con cualquier número de fotos.
  3. `sesiones` (`sesiones`: nombre, texto, precio, duracion, incluye, imagen, destacado): banda clara, filas 50/50 en
     zigzag con la foto a sangre y marcas de visor; número en contorno, precio en serif, «incluye» en dos columnas.
  4. `sobre`: banda primario 50/50 con la foto a sangre, texto y equipo (`personas`); debajo, la `declaracion` en
     banda de acento con la frase enorme en serif.
  5. `proceso`: banda negra; los pasos como fotogramas de una tira con perforaciones arriba y abajo.
  6. `opiniones`: banda clara; la primera opinión enorme en serif y el resto en tres columnas con filetes.
  7. `cta`: banda con foto de fondo y velo lateral, título enorme y dos botones (sin foto, banda de acento).
  8. `preguntas`: banda negra; título fijo a la izquierda y acordeón con botón «+» cuadrado a la derecha.
  9. `contacto`: banda primario; email enorme, datos, y formulario mailto con «Qué necesitas» (nombres de las sesiones)
     y fecha aproximada.
  Pie negro con cuatro columnas y el nombre gigante en contorno.
- **Fotos** (`fotos.json`, 15): costa cantábrica en hora azul para el hero; galería variada (barrio de pescadores bajo la
  lluvia, manos con alianzas en blanco y negro, figura de espaldas frente al mar, producto sobre negro, montaña con
  niebla, set de rodaje vacío, niños de espaldas en la orilla, puerto de noche); una por sesión; mesa del estudio con
  negativos; estudio en penumbra con haz de luz. Sin texto legible, sin logotipos, sin caras reconocibles.
- **Qué no hacer**: tarjetas blancas con sombra, columnas estrechas, huecos en el mosaico, fotos con margen alrededor
  en escritorio, más de un color de acento.

## Hecho

- [x] `site.yaml` de ejemplo (Nordés Estudio, Gijón; teléfonos ficticios), todo activo y relleno, listas planas.
- [x] Secciones nuevas (`galeria`, `sesiones`, `sobre`, `proceso`, `opiniones`, `cta`) y `hero`, `preguntas`,
      `contacto`, `texto`, 404 y aviso legal rediseñados; quitadas `proyectos`, `servicios` y `sobre-nosotros`.
- [x] `template.yaml` con sectores con nombre, secciones y guion del asistente (10 pasos).
- [x] `fotos.json` y placeholders SVG con el mismo nombre.
- [x] `README.md` y `CLAUDE.md`.
- [ ] Fotos y previews (`preview/card.jpg`, `preview/full.jpg`) definitivas: las hace el paso de fotos.
