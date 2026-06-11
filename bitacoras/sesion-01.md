# Bitácora — Sesión 1 (2026-06-10)

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
