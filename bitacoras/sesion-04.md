# Bitácora — Sesión 4 (2026-06-11)

### Contexto

Inicio formal del paso de tarjeta personal a sitio web profesional. Se definió la arquitectura y se implementó la primera versión.

---

### Etapa 18 — Definir la arquitectura del sitio

Antes de escribir código se tomaron decisiones de estructura:

**¿Una página o múltiples páginas?**

En HTML puro sin sistema de plantillas, tener varios archivos `.html` significa duplicar la navegación en cada uno. Si se cambia un link en el menú, hay que actualizarlo en todos los archivos. La solución para esta etapa: **una sola página scrollable con secciones y navegación por anclas** (`#hero`, `#about`, `#projects`, `#contact`). Cuando se incorpore JavaScript o un generador de sitios, la separación en páginas tendrá sentido.

**¿Qué nivel de ambición?**

`PROFILE.md` (sección 17) propone tres niveles. Se eligió el nivel intermedio: una sola página con varias secciones bien estructuradas, sin saltar todavía a funcionalidades dinámicas.

**Estructura adoptada:**

```
<header>  — Barra de navegación sticky
#hero     — Nombre + tagline + foto + CTA
#about    — Bio completa + datos en tres columnas
#projects — Cuatro proyectos destacados en grid
#contact  — Links de redes y correo
<footer>  — Crédito mínimo
```

---

### Etapa 19 — Reescritura de `index.html` y `style.css`

**HTML:** reescritura completa del `<body>`. Se conservaron intactos el `<head>`, meta tags y favicon.

**CSS:** refactorización total. Se conservaron las variables CSS (`:root`) y la paleta de colores. El layout pasó de una tarjeta centrada (`display: flex` en el body) a un sistema de secciones con máximo de ancho (`max-width: 960px`) y navegación sticky.

Nuevos patrones de CSS usados:

- `position: sticky; top: 0` — el header se queda fijo al hacer scroll
- `min-height: calc(100vh - var(--nav-height))` — el hero ocupa la pantalla completa descontando la barra de navegación
- `grid-template-columns: repeat(2, 1fr)` — grid de dos columnas para los proyectos
- `@media (max-width: 640px)` — breakpoint para colapsar a una columna en móvil

---

### Etapa 20 — Refinamiento del hero y eliminación de redundancia

El primer intento del hero tenía cuatro líneas de credenciales seguidas de un párrafo bio que decía lo mismo. El diagnóstico: demasiada información apilada sin jerarquía visual clara.

**Solución:** separar responsabilidades entre secciones.

- **Hero** → impacto inmediato: nombre grande, tagline de tres palabras, ubicación, dos botones.
- **About** → profundidad: el párrafo bio completo y tres columnas con información no redundante.

El tagline del hero quedó: *Trombonista · Ingeniero Físico · Investigador* — tres palabras que capturan el perfil completo sin repetir la bio.

Las tres columnas del about tienen contenido exclusivo:
1. **Formación** — los cuatro títulos académicos como lista
2. **Trayectoria internacional** — los escenarios reales (Bregenz, Rheingau, Tchaikovsky, etc.)
3. **Gestión cultural** — Simposio Internacional de Trombón y Colectivo Colombiano de Trombones

> **Principio aprendido:** cada sección debe tener una razón de existir distinta. Si dos secciones dicen lo mismo, sobra una.

---

### Etapa 21 — Decisión de diseño: sin emojis

En un intento inicial se añadieron emojis como viñetas en la lista de formación (🎺 ⚙️ 🎓 💻). Se descartaron en favor de un guion largo tipográfico (—) en color acento, generado por CSS con `::before`.

Razón: los emojis varían entre sistemas operativos y rompen la consistencia del diseño. Un marcador tipográfico es más estable, más elegante y coherente con la paleta oscura del sitio.

```css
.formation-list li::before {
  content: "—";
  color: var(--color-accent);
}
```

---

### Etapa 22 — Cuatro proyectos destacados

Se eligieron los cuatro proyectos más representativos de las distintas facetas del perfil:

| Proyecto | Categoría | Por qué |
|---|---|---|
| Orquesta Departamental de Antioquia | Orquestal | Cargo actual, mayor visibilidad |
| Simposio Internacional de Trombón | Gestión | Proyecto propio de mayor escala |
| Music Technology Group · UPF | Investigación | Trabajo académico actual |
| Colectivo Colombiano de Trombones | Cámara | Logro con respaldo institucional (Ministerio de Cultura) |

Cada card muestra: tag de categoría, título, rol con fecha y descripción breve.

---

### Estado al cierre de sesión 4

- [x] Arquitectura de página scrollable definida e implementada
- [x] Header sticky con navegación por anclas
- [x] Sección Hero: nombre + tagline + ubicación + CTAs + foto
- [x] Sección About: bio completa + Formación + Trayectoria + Gestión
- [x] Sección Proyectos: grid 2×2 con cuatro proyectos destacados
- [x] Sección Contacto: cinco links de redes
- [x] Footer mínimo
- [x] Diseño responsive (colapsa a una columna en móvil)
- [x] Diseño elegante sin emojis

### Próximas etapas

- [ ] Sección "Lo que enseño" (áreas de docencia)
- [ ] Timeline de trayectoria orquestal
- [ ] Sección de Media / Videos
- [ ] CV descargable (PDF)
- [ ] Blog
