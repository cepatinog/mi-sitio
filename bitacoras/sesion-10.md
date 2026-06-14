# Bitácora — Sesión 10 (2026-06-13)

### Contexto

El sitio creció rápido en las últimas sesiones (Proyectos de 4 → 7 tarjetas, Media a 12 videos) y
empezó a notarse el costo de crecer sin podar: contenido repetido entre secciones y una jerarquía
plana donde todo pesa igual. Tras añadir **un video más a Media** (la presentación de Carlos en la
Academia de Orquestas Latinoamericanas del Teatro del Lago), se abrió una sesión de **optimización**.

Lo interesante del proceso: antes de tocar código se usó **modo plan** y un cuestionario de tres
decisiones para fijar el rumbo editorial —(1) énfasis: *perfil dual* música + tecnología; (2)
alcance: *de-dup + jerarquía* sin reordenar secciones; (3) densidad: *mantener todo* el contenido—.
Recién con esas decisiones se escribió el plan y se implementó.

> **Principio aprendido:** en un sitio de contenido, primero se planea la *información*, no el
> código. Decidir qué se destaca y qué se repite es una decisión editorial; el HTML/CSS solo la
> ejecuta. Modo plan sirvió para separar "qué quiero comunicar" de "cómo lo implemento".

---

### Etapa 39 — De-duplicación: una fuente, un lugar

Una auditoría del sitio mostró la misma entidad repetida en varias secciones: la bio enumeraba los
mismos escenarios que el recuadro "Trayectoria internacional"; la tarjeta de MTG nombraba
"(JamFormer)" que ya tiene tarjeta propia; el logro de gestión cultural aparecía casi idéntico en
*Sobre mí* y en *Docencia*.

La regla aplicada: **cada dato tiene un solo hogar; los demás lugares lo enmarcan, no lo repiten.**

- La **bio** pasó a dar posicionamiento ("festivales y salas de Europa y Latinoamérica") y el
  recuadro **"Trayectoria internacional"** quedó como dueño único de la lista de salas.
- El recuadro **"Gestión cultural"** se reescribió como *logro propio* (con los roles: co-creador,
  representante legal), distinto del *caso de estudio pedagógico* de la tarjeta de Docencia.
- Se quitó "(JamFormer)" de la tarjeta de MTG; la tarjeta dedicada es la dueña del nombre.

Matiz decidido con el usuario: la de-duplicación es **de texto**, no de elementos. Se mantienen los
12 videos y las 8 entradas de timeline. Eso implica aceptar conscientemente que Media siga
mostrando algún video que también aparece enlazado en Proyectos: se prioriza la completitud.

> **Principio aprendido:** "evitar redundancias" no es lo mismo que "borrar todo lo repetido".
> Hay repetición que molesta (texto calcado) y repetición que sirve (un video accesible desde dos
> rutas). El criterio lo pone el objetivo, no una regla mecánica. Y para el texto biográfico:
> ceñirse a datos verificables, sin añadir matices narrativos que no estén en la fuente.

---

### Etapa 40 — Jerarquía: hacer legible el perfil dual

El problema no era falta de contenido sino falta de **jerarquía**: 7 tarjetas de proyectos en una
rejilla plana no dejaban ver de un vistazo las dos facetas (música y tecnología).

Solución, reutilizando un patrón que ya existía en Media (títulos de grupo):

- **Proyectos se dividió en dos clústeres etiquetados** — "Interpretación y gestión cultural" y
  "Tecnología e investigación" — con igual billing para no inclinar la balanza.
- Cada clúster **abre con una tarjeta destacada** (ODA y MTG-UPF) a ancho completo.

Para no duplicar CSS, la clase `.media-group-title` se **generalizó a `.group-title`**, compartida
ahora por Media y Proyectos. La tarjeta destacada usa el grid:

```css
.project-card--featured {
  grid-column: 1 / -1;   /* ocupa de la primera a la última columna */
  border-color: var(--color-accent);
}
```

También se actualizaron los **metadatos** (`title`, `description`, `og:description`), que hasta
ahora describían solo al músico, para reflejar el perfil dual (se añadió el Máster en Sound and
Music Computing de la UPF).

> **Principio aprendido:** la jerarquía es comunicación. Agrupar + destacar guía el ojo sin que el
> visitante tenga que leerlo todo. Y cuando una clase sirve en dos sitios (`.group-title`), vale más
> generalizarla que copiarla: un solo patrón, una sola fuente de estilo.

---

### Estado al cierre de sesión 10

- [x] Video de la presentación en Teatro del Lago añadido a Media
- [x] Texto repetido eliminado (bio↔salas, MTG↔JamFormer, gestión cultural)
- [x] Proyectos en dos clústeres etiquetados con tarjeta destacada por faceta
- [x] Clase `.group-title` compartida (Media + Proyectos) y `.project-card--featured`
- [x] Metadatos coherentes con el perfil dual músico-investigador

### Próximas etapas

- [ ] Posible doble uso del título "Tecnología e investigación" (en Proyectos y en Media)
- [ ] Revisar la repetición Media↔Proyectos si en algún momento se prefiere curar
- [ ] Blog / escritura (sigue pendiente)
