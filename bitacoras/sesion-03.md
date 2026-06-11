# Bitácora — Sesión 3 (2026-06-11)

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

### Etapa 17 — Reorganización de bitácoras

Las sesiones anteriores vivían todas en un solo `BITACORA.md`. A medida que el proyecto crece, un único archivo se vuelve difícil de navegar.

**Nueva estructura:**

```
bitacoras/
  sesion-01.md
  sesion-02.md
  sesion-03.md
  ...
BITACORA.md  ← índice con links a cada sesión
```

`BITACORA.md` quedó como documento de entrada: describe el proyecto, lista las sesiones y enlaza a cada archivo. El contenido detallado vive en archivos individuales.

> **Criterio:** una sesión por archivo. El orden cronológico tiene valor pedagógico — permite ver la evolución del proyecto desde el principio.

---

### Estado al cierre de sesión 3

- [x] Estructura `assets/` organizada (css, images)
- [x] Variables CSS centralizadas en `:root`
- [x] Favicon SVG con iniciales CP
- [x] Open Graph meta tags configurados
- [x] Proyecto renombrado a `mi-sitio` en GitHub y en local
- [x] Bitácoras reorganizadas en carpeta `bitacoras/` por sesión

### Próximas etapas

- [ ] Evaluar si añadir el link al portafolio en Google Drive
- [ ] Añadir sección de proyectos
- [ ] Explorar sección de música / audio
- [ ] Introducir JavaScript cuando haya una necesidad concreta
