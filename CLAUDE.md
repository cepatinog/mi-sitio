# CLAUDE.md — mi-sitio

## Sobre el proyecto

Página web personal de Carlos Patiño (Músico · Trombonista / Ingeniero Físico).
Sirve tres propósitos en paralelo: presencia en internet, portafolio, y espacio de aprendizaje de desarrollo web.

Desplegada en GitHub Pages: https://cepatinog.github.io/mi-sitio

## Stack actual y evolución prevista

El proyecto crece de forma progresiva. No saltar etapas sin que el usuario lo decida:

1. **Etapa actual:** HTML + CSS puro
2. **Siguiente:** JavaScript vanilla (interactividad básica)
3. **Futuro:** Frameworks frontend (evaluar según necesidad)
4. **Largo plazo:** Funcionalidades con Python (posiblemente un backend ligero)

No proponer tecnologías de etapas superiores hasta que la etapa actual esté consolidada.

## Secciones previstas

La página crecerá con estas secciones (orden tentativo):
- Tarjeta principal (actual)
- Proyectos (ingeniería y música)
- Música / Audio (reproductor, grabaciones, links a plataformas)
- Blog / Escritura
- CV / Hoja de vida (con PDF descargable)

## Contenido y voz

`PROFILE.md` es la fuente única de verdad sobre Carlos Patiño. Lee ese archivo antes de escribir cualquier texto del sitio (bio, descripciones, proyectos, secciones). No inventes datos, logros ni tono — tómalos de ahí. Para tareas técnicas (CSS, HTML, git) no es necesario leerlo.

El archivo es local y está en `.gitignore` — nunca se sube al repositorio.

## Idioma de trabajo

- **Conversación:** español
- **Código, variables, funciones:** inglés
- **Commits:** inglés, formato imperativo (`Add hero section`, `Fix nav alignment`)
- **Comentarios en código:** solo cuando el porqué no es obvio; en inglés

## Restricciones — nunca sin permiso explícito

- **No hacer `git push`** bajo ninguna circunstancia sin que el usuario lo pida en ese momento
- **No instalar dependencias** (npm, pip, etc.) sin aprobación previa del usuario
- **No crear ni modificar archivos fuera de la carpeta del proyecto**
- **No cambiar el diseño visual** de forma significativa sin consultarlo primero

## Flujo de trabajo esperado

1. Explicar el enfoque antes de implementar si el cambio es no trivial
2. El usuario revisa los archivos modificados antes de commitear
3. El usuario decide cuándo y qué se sube a GitHub
4. Al finalizar cada sesión, actualizar `BITACORA.md` con lo trabajado

## Bitácora

`BITACORA.md` es un documento pedagógico público — va al repositorio. Por eso:
- No incluir información personal (emails, teléfonos, datos privados)
- Sí incluir decisiones técnicas, razonamiento, comandos y aprendizajes
- Actualizar al cierre de cada sesión, antes del último commit
