# Bitácora — Sesión 6 (2026-06-13)

### Contexto

Inicio de la Parte B del roadmap: añadir secciones de contenido nuevas, todo en
HTML/CSS puro (etapa 1). En esta sesión se sumaron **Docencia** y **Media / Videos**,
y se aprendió a previsualizar correctamente embeds de YouTube en local.

---

### Etapa 26 — Sección "Lo que enseño" (Docencia)

Nueva sección `#teaching` entre Proyectos y Contacto, con un grid de seis tarjetas
(una por cada área de docencia del `PROFILE.md` §9): trombón, gestión cultural,
tecnología musical, física del sonido, diseño de portafolios y producción de audio.

Reutiliza el patrón visual de `.project-card` y usa el grid auto-responsive aprendido
en la sesión 5 (`repeat(auto-fit, minmax(240px, 1fr))`), así que colapsa sola en
pantallas pequeñas sin añadir media queries.

> **Principio aprendido:** una vez que un patrón (la card con borde y hover de acento)
> está resuelto, las secciones nuevas se construyen reutilizándolo. La consistencia
> visual sale gratis y el CSS no crece de forma desordenada.

---

### Etapa 27 — Sección Media / Videos (galería de embeds)

Nueva sección `#media` con once videos de YouTube agrupados en tres bloques:
**Interpretación** (5), **Proyectos propios** (3) y **Tecnología e investigación** (3).

Decisiones técnicas:

- **Embeds responsivos sin JavaScript:** cada video va en un contenedor con
  `aspect-ratio: 16 / 9` y un `<iframe>` que llena el 100%. El `aspect-ratio` moderno
  reemplaza al viejo truco del `padding-bottom: 56.25%`.
- **`loading="lazy"`** en cada iframe: es un atributo HTML (no JS) que difiere la carga
  de los videos que están fuera de la pantalla. Clave para que una galería de once
  embeds no penalice el tiempo de carga inicial.
- **`youtube-nocookie.com`** como dominio de embed: no instala cookies de seguimiento
  hasta que la persona pulsa play.
- Grid `auto-fit/minmax(280px, 1fr)` por bloque, con subtítulos de categoría.

---

### Etapa 28 — Error 153: por qué los embeds fallan al abrir el HTML como archivo

Al previsualizar abriendo el archivo directamente (`file://` / ruta `wsl.localhost/...`),
todos los videos mostraban **"Error 153 — Error de configuración del reproductor"**.

Causa: los embeds de YouTube validan el **origin** (el dominio desde el que se cargan).
Un archivo local no tiene origin HTTP, así que YouTube rechaza la reproducción.

Solución: servir el sitio por HTTP en lugar de abrirlo como archivo.

```bash
python3 -m http.server 8000 --directory /ruta/al/proyecto
# luego abrir http://localhost:8000  (NO la ruta de archivo)
```

> **Principio aprendido:** muchos comportamientos web (embeds, fetch, rutas relativas,
> service workers) dependen del **origin** y solo funcionan servidos por HTTP. Abrir el
> `.html` con doble clic no es equivalente a visitarlo en un servidor. En producción
> (GitHub Pages, HTTPS) el problema no existe.

---

### Etapa 29 — Verificar los IDs de YouTube con la API oEmbed

Un video no cargaba porque su ID estaba mal transcrito desde el PDF del portafolio:
el carácter `l` (L minúscula) y `I` (i mayúscula) se ven idénticos en muchas tipografías
(`...CLlrE` debía ser `...CLIrE`).

Para descartar más errores se verificaron los once IDs de una sola vez contra la API
pública de YouTube, que además devuelve el título real de cada video:

```bash
curl -s "https://www.youtube.com/oembed?format=json&url=https://www.youtube.com/watch?v=$ID"
```

Esto reveló dos cosas: (1) el ID corregido ya resolvía, y (2) un video etiquetado como
"Gran Concierto Davivienda" era en realidad el videoclip sinfónico de Diego Torres
("Tratar de Estar Mejor"), por lo que se reetiquetó para que el texto coincida con el
contenido real.

> **Principio aprendido:** copiar identificadores desde un PDF es propenso a errores por
> caracteres ambiguos (`l`/`I`, `O`/`0`, `1`/`l`). Conviene verificarlos automáticamente
> contra la fuente (aquí, la API oEmbed), que de paso confirma que cada enlace apunta a
> lo que se cree.

---

### Estado al cierre de sesión 6

- [x] Sección Docencia (6 áreas)
- [x] Sección Media (11 videos en 3 bloques, embeds diferidos)
- [x] Embeds verificados contra la API oEmbed; textos alineados al contenido real
- [x] Aprendido el flujo de previsualización por HTTP para evitar el Error 153

### Próximas etapas

- [ ] **Timeline** de trayectoria orquestal e internacional (será el 7º enlace del menú)
- [ ] **CV / portafolio descargable** en PDF

> Punto de decisión que se acerca: con un 7º enlace, el menú dejará de caber cómodamente
> en móvil. Ese será el momento de introducir **JavaScript** (menú hamburguesa) y dar el
> salto a la etapa 2 del proyecto.
