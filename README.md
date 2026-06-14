# mi-sitio

Página web personal de **Carlos Patiño** — Trombonista · Ingeniero Físico · Investigador · Docente.

🔗 **En vivo:** https://cepatinog.github.io/mi-sitio

---

## Qué es esto

Un sitio personal que cumple tres propósitos a la vez:

- **Presencia en internet** — un lugar propio, no una red social.
- **Portafolio** — trayectoria, proyectos, docencia y media en un solo sitio.
- **Espacio de aprendizaje** — construido desde cero como ejercicio de desarrollo web,
  documentado paso a paso en la [bitácora](BITACORA.md).

Sin frameworks ni build tools: HTML, CSS y JavaScript vanilla servidos directamente por
GitHub Pages.

## Stack

El proyecto crece por etapas, sin saltarse ninguna:

1. **HTML + CSS puro** — ✅ consolidada
2. **JavaScript vanilla** — ← etapa actual (menú hamburguesa, scrollspy, tema claro/oscuro)
3. Frameworks frontend — futuro
4. Python / backend ligero — largo plazo

Sin dependencias: el sitio es un conjunto de archivos estáticos. El tema (claro/oscuro)
se persiste en `localStorage` y los videos se incrustan con `youtube-nocookie.com`.

## Estructura

```
index.html            Sitio principal (una página, secciones + nav sticky)
cv.html               Hoja de vida navegable (documento aparte)
assets/
  css/style.css       Estilos del sitio (tema claro/oscuro)
  css/cv.css          Estilos del CV (2 columnas, con @media print)
  js/main.js          Menú hamburguesa, scrollspy, toggle de tema
  images/foto.jpg     Retrato principal
bitacoras/            Una bitácora por sesión (sesion-NN.md)
README.md             Este archivo
BITACORA.md           Índice de bitácoras
```

> Los documentos fuente con datos personales (perfil de contenido, CV y portafolio en PDF)
> viven en `_local/`, fuera del control de versiones. No se publican.

## Previsualización local

Servir por HTTP (no abrir el `.html` con doble clic):

```bash
python3 -m http.server 8000 --directory .
# luego abrir http://localhost:8000
```

Abrir como `file://` rompe los embeds de YouTube (Error 153): necesitan un *origin* HTTP
válido. En GitHub Pages funcionan sin problema.

## Bitácora

El proceso de construcción está documentado sesión a sesión en
[`BITACORA.md`](BITACORA.md) y la carpeta [`bitacoras/`](bitacoras/) — decisiones técnicas,
dudas, comandos y aprendizajes. Escrita para entender *cómo* se hizo, no solo *qué* quedó.

---

© Carlos Patiño · Medellín, Colombia
