# Bitácora — Sesión 11 (2026-06-13)

### Contexto

Sesión corta y visual: explorar cómo se vería la foto del hero **más grande y en otro formato**,
sin perder el minimalismo. El método fue exploratorio — se compararon tres formatos antes de tocar
código y luego se afinó el resultado en vivo.

---

### Etapa 41 — La foto del hero: de círculo a retrato

La foto nació como un **círculo** de 200×200 (`border-radius: 50%`). Se evaluaron tres alternativas
—retrato vertical, arco superior y cuadrado suave— y se eligió el **retrato vertical 3:4**, un
formato editorial que muestra más de la persona.

La regla quedó así:

```css
.hero-photo img {
  width: 260px;
  max-width: 100%;     /* nunca desborda en pantallas pequeñas */
  aspect-ratio: 3 / 4; /* la altura se deduce del ancho */
  border-radius: 40px;
  object-fit: cover;   /* recorta para llenar sin deformar */
  display: block;
  outline: 3px solid var(--color-border);
  outline-offset: 4px;
}
```

Tres piezas hacen el trabajo:

- **`aspect-ratio: 3 / 4`** fija la proporción sin necesidad de declarar la altura a mano; si cambia
  el ancho, la altura se recalcula sola.
- **`object-fit: cover`** rellena el marco recortando lo que sobra, en vez de deformar la imagen.
- **`max-width: 100%`** evita que el retrato (más alto que el círculo) desborde en móvil, donde la
  foto pasa arriba y se centra.

El redondeo se ajustó **en vivo** (18 → 28 → 40 px) recargando el sitio servido en local, hasta dar
con el punto preferido. Un solo bloque de CSS tocado; nada más del layout cambió.

> **Principio aprendido:** para una proporción fija, `aspect-ratio` + `object-fit: cover` es más
> robusto que fijar `width` y `height` a mano: se adapta solo y nunca deforma la foto. Y para
> decisiones de diseño, iterar sobre el sitio servido (no sobre suposiciones) es la forma rápida de
> elegir un valor.

> **Nota de taller (previsualización):** servir con `python3 -m http.server` y refrescar es el ciclo
> de prueba. Dos tropiezos del entorno: `sleep` en primer plano está bloqueado (usar tareas en
> segundo plano), y `pkill -f "http.server 8000"` se mata a sí mismo porque ese texto también está
> en la línea de comando de la propia shell — mejor liberar el puerto con otra herramienta.

---

### Estado al cierre de sesión 11

- [x] Foto del hero en formato retrato vertical 3:4 (~260×347), más grande que el círculo
- [x] Esquinas redondeadas a 40px, contorno sutil conservado
- [x] Responsive sólido (`aspect-ratio`, `object-fit: cover`, `max-width: 100%`)

### Próximas etapas

- [ ] Posible ajuste de encuadre con `object-position` si el recorte vertical lo pide
- [ ] Blog / escritura (sigue pendiente)
