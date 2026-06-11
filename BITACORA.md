# Bitácora — mi-tarjeta

Documento de aprendizaje personal. Registra el proceso de construir esta página web desde cero, incluyendo decisiones, dudas, herramientas y razonamiento detrás de cada etapa. Escrito para el yo del futuro — y para cualquier persona que encuentre útil leer un proceso real, no idealizado.

---

## Sesión 1 — 2026-06-10

### Contexto de partida

Primera vez usando **Claude Code** (CLI de Anthropic que permite trabajar con un asistente de IA directamente desde el terminal y el editor de código). El objetivo no era solo hacer una página web, sino entender el flujo de trabajo real y las implicaciones de usar una herramienta de este tipo.

Entorno: WSL (Windows Subsystem for Linux) + VS Code.

---

### Etapa 1 — Decidir qué construir

Antes de escribir una sola línea de código, se definió qué construir y con qué criterios:

- **Tipo de página:** tarjeta personal (nombre, descripción, links)
- **Estilo:** minimalista oscuro
- **Stack inicial:** HTML + CSS puro — sin frameworks, sin JavaScript
- **Razón:** empezar desde lo más simple posible para entender cada pieza antes de añadir complejidad

> **Aprendizaje:** definir el alcance antes de empezar evita sobreingeniería. Una página simple bien hecha es mejor punto de partida que una compleja a medias.

---

### Etapa 2 — Crear los archivos

Claude Code creó dos archivos:

**`index.html`** — estructura de la página (HTML semántico)
**`style.css`** — estilos separados del HTML

La separación HTML/CSS es una convención estándar: el HTML define *qué* hay en la página, el CSS define *cómo* se ve. Mezclarlos (usando el atributo `style=` directamente en HTML) funciona pero dificulta el mantenimiento.

---

### Etapa 3 — Elegir dónde publicar

Opciones evaluadas para alojar la página de forma gratuita:

| Opción | Pros | Contras |
|---|---|---|
| **GitHub Pages** | Estándar, integrado con git, gratis | Requiere saber git |
| **Netlify Drop** | Rapidísimo, sin cuenta necesaria | Menos estándar, menos control |

**Decisión: GitHub Pages.** Razón principal: el flujo con git es el que se usa en proyectos reales, y aprenderlo desde el principio tiene más valor a largo plazo.

---

### Etapa 4 — Control de versiones con git

Git es un sistema que registra la historia de cambios de un proyecto. Cada `commit` es una fotografía del estado del código en un momento dado.

Comandos usados:

```bash
git init                        # inicializa el repositorio local
git add index.html style.css   # selecciona los archivos a registrar
git commit -m "Add personal card page"  # guarda la fotografía con un mensaje
git branch -m main             # renombra la rama principal a "main" (estándar actual)
```

> **Por qué `main` y no `master`:** GitHub adoptó `main` como nombre por defecto en 2020. Renombrarlo evita confusión al conectar con GitHub.

---

### Etapa 5 — Conectar con GitHub y publicar

```bash
git remote add origin git@github.com:cepatinog/mi-tarjeta.git
git push -u origin main
```

- `remote add origin` le dice a git local dónde está el repositorio remoto
- `push` sube los commits locales a GitHub
- La URL `git@github.com:...` usa SSH — aprovecha una clave que ya estaba configurada en el sistema (Claude Code no vio ni usó credenciales directamente)

Luego, en GitHub: `Settings > Pages > Deploy from branch: main / root`.

**Resultado:** página disponible en `https://cepatinog.github.io/mi-tarjeta`

Cada `git push` futuro actualiza la página automáticamente.

---

### Etapa 6 — Seguridad y acceso

Pregunta importante planteada durante la sesión: **¿a qué tiene acceso Claude Code?**

Respuesta honesta:
- Tiene acceso al sistema de archivos con los permisos del usuario que lo ejecuta
- Puede correr comandos bash — cada uno es visible y aprobable antes de ejecutarse
- No tiene acceso a contraseñas ni tokens de GitHub (usó la clave SSH ya existente)
- No actúa entre sesiones — solo cuando el usuario está presente

> **Regla práctica:** tratar a Claude Code como un desarrollador con acceso a tu computador. Útil, pero requiere atención. Nunca aprobar comandos que no se entienden.

---

### Etapa 7 — Documentar el proyecto con `CLAUDE.md`

`CLAUDE.md` es un archivo que Claude Code lee automáticamente al inicio de cada sesión. Sirve para dar contexto del proyecto sin tener que repetirlo cada vez.

**Qué incluye en este proyecto:**
- Propósito de la página
- Stack actual y evolución prevista (HTML → JS → frameworks → Python)
- Secciones futuras planeadas
- Convenciones de idioma (conversación en español, código en inglés)
- Restricciones explícitas: no push sin permiso, no instalar dependencias sin aprobación, no salir de la carpeta del proyecto

> **Por qué es importante:** el contexto escrito por el usuario es siempre más preciso que el que infiere la IA. `CLAUDE.md` es control explícito sobre cómo trabaja el asistente.

---

---

### Etapa 8 — Foto de perfil y links reales

Se reemplazaron los placeholders (`#`) por los links reales y las iniciales "CP" por una fotografía.

**Decisión sobre la foto:** en lugar de apuntar a la URL de LinkedIn, se descargó el archivo localmente con `curl` y se incluyó en el repositorio como `foto.jpg`.

```bash
curl -L "URL-de-linkedin" -o foto.jpg
```

Razón: las URLs de LinkedIn tienen fecha de expiración. Una imagen referenciada externamente puede dejar de funcionar sin aviso. Al vivir en el repositorio, la foto es permanente e independiente de terceros.

**¿Es buena práctica subir imágenes a GitHub?**

Depende del tamaño y la cantidad. Git está optimizado para texto — los binarios no tienen diff significativo y cada versión se almacena completa. Para un archivo pequeño (~100KB) en un sitio personal, es aceptable. A escala se usan Git LFS o CDNs externos.

| Situación | Solución |
|---|---|
| Pocos assets pequeños | En el repo — está bien |
| Muchos assets o archivos grandes | Git LFS |
| Sitio con tráfico real | CDN externo |

**Cambio en CSS:** `.avatar` pasó de ser un `<div>` con iniciales a un `<img>` circular usando `object-fit: cover` y `border-radius: 50%`.

---

### Etapa 9 — Contexto de perfil con PROFILE.md

Se decidió crear un documento de perfil profesional detallado (`PROFILE.md`) como fuente única de verdad para el contenido del sitio.

**Problema:** el repositorio es público. Subir un documento personal extenso lo haría indexable por buscadores.

**Solución:** mantenerlo solo de forma local usando `.gitignore`.

```bash
# .gitignore
PROFILE.md
```

`.gitignore` le indica a git qué archivos debe ignorar — existen en el sistema local pero nunca se suben al repositorio remoto.

`CLAUDE.md` se actualizó con la instrucción de leer `PROFILE.md` antes de escribir cualquier contenido del sitio, y aclarando que no es necesario para tareas técnicas (CSS, HTML, git).

---

### Etapa 10 — Convenciones de bitácora

Se estableció que `BITACORA.md` es público y pedagógico. Reglas definidas:
- No incluir información personal
- Documentar decisiones técnicas, razonamiento y aprendizajes
- Actualizar al cierre de cada sesión de trabajo

Estas reglas quedaron registradas en `CLAUDE.md` para que apliquen automáticamente en sesiones futuras.

---

### Estado al final de la sesión

- [x] Página web creada y funcionando
- [x] Repositorio en GitHub con historial de commits
- [x] Publicada en GitHub Pages
- [x] Foto de perfil real y links funcionales
- [x] `CLAUDE.md` con contexto, reglas de trabajo y convenciones de bitácora
- [x] `.gitignore` configurado para proteger `PROFILE.md`
- [x] `PROFILE.md` disponible localmente como fuente de contenido
- [x] `BITACORA.md` como documento pedagógico público

### Próximas etapas

- [ ] Añadir bio corta a la tarjeta (usando PROFILE.md como fuente)
- [ ] Añadir sección de proyectos
- [ ] Explorar sección de música / audio
- [ ] Introducir JavaScript cuando haya una necesidad concreta

---

## Sesión 2 — 2026-06-10 (continuación)

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

### Estado al cierre de sesión 2

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

---

---

## Sesión 3 — 2026-06-11

### Etapa 14 — Reorganización en carpeta `assets/`

Los archivos CSS y la foto de perfil vivían en la raíz del proyecto junto con `index.html`. A medida que un sitio crece, esto se vuelve difícil de mantener.

Se movieron a una estructura de carpetas estándar:

```
assets/
  css/
    style.css
  images/
    foto.jpg
```

Se actualizaron los paths en `index.html` para reflejar el nuevo lugar de cada archivo:

```html
<link rel="stylesheet" href="assets/css/style.css">
<img src="assets/images/foto.jpg" ...>
```

> **Aprendizaje:** organizar assets desde el principio tiene cero costo ahora y evita refactorizaciones dolorosas más adelante. La estructura `assets/css/`, `assets/images/`, `assets/js/` es una convención ampliamente usada.

---

### Etapa 15 — Variables CSS, favicon y Open Graph

**Variables CSS (custom properties):**

Se refactorizó `style.css` para centralizar todos los valores de color en variables al inicio del archivo:

```css
:root {
  --color-bg: #0d0d0d;
  --color-surface: #1a1a1a;
  --color-accent: #3a7bd5;
  /* ... */
}
```

Antes de esto, el mismo color podía aparecer repetido en 10 reglas distintas. Si se quería cambiar el azul de acento, había que buscar y reemplazar en todo el archivo. Ahora basta con cambiar una línea.

**Favicon SVG:**

Se añadió un favicon (el ícono que aparece en la pestaña del navegador) usando un SVG inline en el `<head>`. Contiene las iniciales "CP" sobre un fondo oscuro, coherente con el diseño de la tarjeta. No requiere un archivo externo — el SVG va codificado directamente en el atributo `href`.

**Open Graph meta tags:**

Open Graph es un protocolo creado por Facebook, adoptado por casi todas las plataformas sociales, que define cómo se ve una página cuando alguien la comparte en redes:

```html
<meta property="og:title" content="Carlos Patiño">
<meta property="og:description" content="...">
<meta property="og:image" content="...">
<meta property="og:url" content="...">
```

Sin estas etiquetas, Twitter, WhatsApp o LinkedIn eligen arbitrariamente qué texto e imagen mostrar al compartir el link. Con ellas, el control queda en manos del autor.

El texto de descripción se tomó de `PROFILE.md` (fuente única de verdad), no se inventó.

---

### Etapa 16 — Renombre del proyecto: `mi-tarjeta` → `mi-sitio`

El nombre original reflejaba el alcance inicial (una tarjeta personal). Con las secciones planeadas (proyectos, música, blog, CV), el nombre quedó pequeño.

**Pasos realizados:**

1. Renombrar el repositorio en GitHub: `Settings > Repository name`
2. Actualizar el remote local para apuntar al nuevo nombre:
   ```bash
   git remote set-url origin git@github.com:cepatinog/mi-sitio.git
   ```
3. Renombrar la carpeta local de `mi-tarjeta` a `mi-sitio`
4. Actualizar las URLs de Open Graph en `index.html` para que apunten a `cepatinog.github.io/mi-sitio`

> **Nota:** GitHub redirige automáticamente el tráfico del repo antiguo al nuevo durante un tiempo, pero las URLs explícitas en el HTML deben actualizarse a mano.

---

### Estado al cierre de sesión 3

- [x] Estructura `assets/` organizada (css, images)
- [x] Variables CSS centralizadas en `:root`
- [x] Favicon SVG con iniciales CP
- [x] Open Graph meta tags configurados
- [x] Proyecto renombrado a `mi-sitio` en GitHub y en local

### Próximas etapas

- [ ] Evaluar si añadir el link al portafolio en Google Drive
- [ ] Añadir sección de proyectos
- [ ] Explorar sección de música / audio
- [ ] Introducir JavaScript cuando haya una necesidad concreta

---

*Este documento se actualiza al final de cada sesión de trabajo.*
