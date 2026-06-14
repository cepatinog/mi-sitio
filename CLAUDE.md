# CLAUDE.md — mi-sitio

## Sobre el proyecto

Página web personal de Carlos Patiño (Trombonista · Ingeniero Físico · Investigador · Docente).
Sirve tres propósitos en paralelo: presencia en internet, portafolio y espacio de aprendizaje de desarrollo web.

Desplegada en GitHub Pages: https://cepatinog.github.io/mi-sitio

## Estructura del proyecto

```
index.html            Sitio principal (una página con secciones + nav sticky)
cv.html               Hoja de vida navegable (documento aparte, abre en pestaña nueva)
assets/
  css/style.css       Estilos del sitio (tema oscuro)
  css/cv.css          Estilos del CV (tema claro, 2 columnas, con @media print)
  js/main.js          JavaScript del sitio (menú hamburguesa, scrollspy)
  images/foto.jpg     Retrato principal
bitacoras/            Una bitácora por sesión (sesion-NN.md)
README.md             Presentación pública del proyecto
BITACORA.md           Índice de bitácoras
_local/               Archivos locales, no se publican (en .gitignore)
  PROFILE.md          Fuente de verdad del contenido
  *.pdf               Documentos fuente (CV, hoja de vida, portafolio)
```

Secciones actuales de `index.html`: hero, about, timeline, projects, teaching, media, contact.
Ideas pendientes: blog / escritura, modo claro-oscuro, filtros en proyectos o media.

## Stack y evolución por etapas

El proyecto crece de forma progresiva. **No saltar de etapa sin que el usuario lo decida.**

1. HTML + CSS puro — ✅ consolidada
2. **JavaScript vanilla — ← etapa actual** (menú hamburguesa, scrollspy)
3. Frameworks frontend — futuro, evaluar según necesidad
4. Funcionalidades con Python / backend ligero — largo plazo

No proponer tecnologías de etapas superiores a la actual sin acordarlo primero.

## Convenciones técnicas adoptadas

Patrones ya establecidos en el proyecto (reutilizarlos por coherencia):

- **Colores y medidas:** variables CSS en `:root` (`--color-*`, `--nav-height`, `--max-width`).
- **Grids responsive:** `repeat(auto-fit, minmax(Xpx, 1fr))` en lugar de breakpoints manuales cuando se puede.
- **Header sticky + anclas:** `scroll-behavior: smooth` y `scroll-padding-top: var(--nav-height)` en `html`.
- **Embeds de video:** `youtube-nocookie.com`, wrapper con `aspect-ratio: 16/9` y `loading="lazy"`.
- **Interactividad (JS):** `IntersectionObserver` para el scrollspy; menú accesible con `aria-expanded` / `aria-controls`.
- **Responsive:** breakpoint principal en `max-width: 640px`.

## Previsualización local

Servir por HTTP (no abrir el `.html` con doble clic):

```
python3 -m http.server 8000 --directory .
# luego abrir http://localhost:8000
```

Abrir como `file://` rompe los embeds de YouTube (Error 153): necesitan un *origin* HTTP válido.
En GitHub Pages funcionan sin problema.

## Contenido y voz

`_local/PROFILE.md` es la **fuente única de verdad** sobre Carlos Patiño. Léelo antes de escribir
cualquier texto del sitio (bio, descripciones, proyectos, secciones). No inventes datos, logros ni
fechas — tómalos de ahí. Para tareas técnicas (CSS, HTML, JS, git) no es necesario.

- **Tono de marca** (PROFILE §15): directo, honesto, sin marketing inflado; datos verificables sobre
  afirmaciones genéricas.
- Documentos fuente adicionales (CV y portafolio en PDF) viven en `_local/`: contienen datos
  personales y están ignorados (`_local/` en `.gitignore`). Nunca se publican.

## Idioma de trabajo

- **Conversación:** español
- **Textos del sitio:** español
- **Código, variables, funciones:** inglés
- **Commits:** inglés, formato imperativo (`Add hero section`, `Fix nav alignment`)
- **Comentarios en código:** solo cuando el porqué no es obvio; en inglés

## Restricciones — nunca sin permiso explícito

- **No hacer `git push`** sin que el usuario lo pida en ese momento.
- **No incluir el trailer `Co-Authored-By`** en los mensajes de commit.
- **No instalar dependencias** (npm, pip, etc.) sin aprobación previa.
- **No publicar PDFs ni datos personales** (teléfono, dirección, cédula).
- **No crear ni modificar archivos fuera de la carpeta del proyecto.**
- **No cambiar el diseño visual** de forma significativa sin consultarlo primero.

## Flujo de trabajo esperado

1. Explicar el enfoque antes de implementar si el cambio es no trivial.
2. El usuario revisa los archivos modificados (suele editarlos a mano) antes de commitear.
3. El usuario decide cuándo y qué se commitea y se sube a GitHub.
4. Al cierre de cada sesión, documentar en `bitacoras/sesion-NN.md` y enlazarla en `BITACORA.md`.

## Bitácora

Documento pedagógico **público** (va al repositorio). Una bitácora por sesión en `bitacoras/`,
con numeración continua de "Etapas". Por eso:

- No incluir información personal (emails, teléfonos, datos privados).
- Sí incluir decisiones técnicas, razonamiento, comandos y aprendizajes.
- Actualizar al cierre de cada sesión, antes del último commit.
