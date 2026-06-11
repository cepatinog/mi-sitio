# Bitácora — Sesión 2 (2026-06-10)

### Etapa 11 — Bio a partir de PROFILE.md

Se creó la bio de la tarjeta tomando el texto directamente de `PROFILE.md` (fuente única de verdad), sin inventar datos.

Se evaluaron tres opciones con lógicas distintas:
- **Datos concretos:** rol actual + centro de investigación
- **La intersección:** descripción de lo que hace único al perfil
- **Híbrida:** rol + ubicación geográfica

Se eligió una versión híbrida ajustada por el usuario:
> *Trombonista principal de la Orquesta Departamental de Antioquia · Investigador en música e inteligencia artificial. Medellín, Colombia.*

La ubicación se separó luego del bio como elemento independiente para mejorar la jerarquía visual.

> **Aprendizaje:** tener una fuente de verdad (PROFILE.md) evita que el asistente invente datos o interprete el perfil de forma reducida. El usuario mantiene control sobre qué dice el sitio sobre él.

---

### Etapa 12 — Mejoras visuales

Se refinó el diseño de la tarjeta en varios frentes:

**Íconos en los enlaces:**
Se usaron SVGs inline (código SVG directamente en el HTML) para los íconos de GitHub, LinkedIn, Instagram, YouTube y Contacto. Esta técnica no requiere dependencias externas ni peticiones de red adicionales — los íconos son parte del archivo HTML.

**Emojis de ubicación:**
Se añadieron 📍 y 🇨🇴 como línea separada del bio. Separar la ubicación del texto descriptivo mejora la legibilidad y da más respiro visual a cada elemento.

**Tipografía y jerarquía:**
- Rol en mayúsculas pequeñas (`text-transform: uppercase`) para diferenciarlo del nombre y la bio
- Bio en gris medio, tamaño cómodo de lectura
- Ubicación en gris oscuro, discreta pero presente

**Avatar:**
Se reemplazó `border` por `outline` con `outline-offset`. La diferencia: `border` forma parte de la caja del elemento y puede afectar proporciones; `outline` se dibuja por fuera sin alterar el layout, logrando un anillo separado limpio.

**Hover en links:**
Al pasar el cursor, el borde cambia a azul y aparece un tinte de fondo sutil (`rgba(58, 123, 213, 0.08)`), dando feedback sin ser agresivo.

---

### Etapa 13 — Instagram y YouTube

Se añadieron los dos canales restantes. El orden final de los links refleja una progresión de lo técnico-profesional a lo personal:
GitHub → LinkedIn → Instagram → YouTube → Contacto

---

### Estado al cierre de sesión

- [x] Bio escrita a partir de PROFILE.md
- [x] Ubicación con emojis como elemento independiente
- [x] Íconos SVG inline en los cinco links
- [x] Tipografía y jerarquía visual refinadas
- [x] Cinco redes / canales enlazados

### Próximas etapas

- [ ] Evaluar si añadir el link al portafolio en Google Drive
- [ ] Añadir sección de proyectos
- [ ] Explorar sección de música / audio
- [ ] Introducir JavaScript cuando haya una necesidad concreta
