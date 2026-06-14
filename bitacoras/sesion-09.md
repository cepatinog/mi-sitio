# Bitácora — Sesión 9 (2026-06-13)

### Contexto

Sesión de mantenimiento y crecimiento del portafolio, dentro de la pausa de la etapa 2 (antes
del blog). Tres frentes: un **README** público para el repo, una **limpieza de la estructura de
carpetas**, y el **enlace de proyectos externos** (demos, paper) desde la sección Proyectos.

---

### Etapa 36 — README del proyecto

Hasta ahora el repo tenía `CLAUDE.md` (guía para el asistente) y `BITACORA.md` (proceso de
aprendizaje), pero no un `README.md`, que es lo primero que ve quien llega al repo en GitHub.

Se escribió en español, coherente con la bitácora, cubriendo: qué es el sitio (presencia +
portafolio + aprendizaje), el stack por etapas, la estructura de carpetas, la previsualización
local y un enlace a la bitácora.

> **Principio aprendido:** los tres documentos de texto del repo tienen audiencias distintas y
> conviene no mezclarlas. `README.md` → quien visita el repo. `CLAUDE.md` → el asistente que
> trabaja en el código. `BITACORA.md` → el registro del proceso. Cada uno responde una pregunta
> diferente: *qué es*, *cómo trabajar aquí*, *cómo se construyó*.

---

### Etapa 37 — Limpieza de la raíz: carpeta `_local/`

La raíz acumulaba archivos **locales** (el `PROFILE.md` con la fuente de contenido y tres PDFs
con datos personales). Estaban ignorados por git, pero igual ensuciaban el directorio de trabajo.

Se movieron todos a una carpeta `_local/` y se simplificó el `.gitignore`: de reglas sueltas
(`PROFILE.md` y `/*.pdf`) a ignorar la carpeta entera, dejando las reglas anteriores solo como
salvaguarda por si algún archivo personal vuelve a caer en la raíz.

```gitignore
# Archivos locales: datos personales y documentos fuente. No se publican.
_local/

# Salvaguardas por si algún archivo personal queda en la raíz
/*.pdf
PROFILE.md
```

Después se actualizó `CLAUDE.md` (diagrama de estructura y rutas a `PROFILE.md`) para que la
documentación no quedara desfasada.

> **Principio aprendido:** que un archivo esté en `.gitignore` no significa que esté *ordenado*.
> Lo ignorado sigue ocupando la raíz. Agrupar lo local en una carpeta con nombre claro mantiene
> el directorio legible. El guion bajo (`_local`) lo ordena arriba y señala "no es parte del
> sitio". Tras mover, se verificó con `git check-ignore` que nada sensible quedara rastreado y
> que git solo viera los cambios esperados.

---

### Etapa 38 — Proyectos enlazables: demo, paper y el patrón `.project-link`

El portafolio creció con tres proyectos propios de música + tecnología y un enlace al Simposio:

- **Armonía Funcional Sonificada** (web educativa, Pyodide + VexFlow) — *Ver demo*.
- **Liquiprism** (autómatas celulares → MIDI, Python) — *Ver demo* + *Paper* (Dorin, ICAD 2002).
- **JamFormer** (transformer de melodías condicionadas por acordes) — *Ver presentación* + *Ver demo*.
- **Simposio Internacional de Trombón** (tarjeta ya existente) — *Ver pitch* del diplomado GLP.

Las tarjetas no tenían enlaces, así que se creó la clase `.project-link`. El detalle interesante
fue de CSS: la descripción se estilizaba con `.project-card p:last-child`. Al añadir un enlace
después de la descripción, esa `<p>` dejó de ser el último hijo y perdía su estilo. La solución
no fue tocar el HTML de las otras tarjetas, sino describir el elemento por su **rol** en vez de su
**posición**:

```css
/* antes: dependía de que la descripción fuera el último hijo */
.project-card p:last-child { ... }

/* después: apunta a la descripción sin importar qué venga después */
.project-card p:not(.project-role) { ... }
```

Para las tarjetas con varios enlaces se usó el selector de hermano adyacente, que separa enlaces
consecutivos sin añadir margen sobrante al primero:

```css
.project-link + .project-link { margin-left: 1.25rem; }
```

Detalles de contenido: las descripciones se tomaron de los repos fuente (no inventadas),
manteniendo el tono de marca; se usaron tags distintos (**Tecnología / Generativo / IA**) para
diferenciar web educativa, autómatas celulares y deep learning; y se quitó el parámetro `?si=`
(rastreo de "compartir") de las URLs de YouTube antes de enlazarlas.

> **Principio aprendido:** un estilo que depende de la *posición* (`:last-child`) se rompe en
> silencio cuando se añaden elementos. Es más robusto seleccionar por lo que el elemento *es*
> (`:not(.project-role)`) que por dónde está. La misma idea, aplicada a contenido: citar datos
> verificables desde la fuente y no inflar.

---

### Estado al cierre de sesión 9

- [x] `README.md` público en español
- [x] Raíz limpia: locales en `_local/`, `.gitignore` y `CLAUDE.md` sincronizados
- [x] Tres proyectos nuevos enlazados (AFS, Liquiprism, JamFormer) + pitch del Simposio
- [x] Patrón `.project-link` reutilizable (uno o varios enlaces por tarjeta)

### Próximas etapas

- [ ] Layout de Proyectos con número impar de tarjetas (7 deja una sola en la última fila)
- [ ] Revisar la repetición de JamFormer (tarjeta propia + mención en MTG-UPF + embed en Media)
- [ ] Blog / escritura (sigue pendiente)
