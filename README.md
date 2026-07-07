# Mientras No Estoy 💌

Calendario de adviento digital de 14 días para Vicky — del 6 al 19 de julio de 2026, mientras Tommy está en Boston. Cartas, juegos, fotos, canción, una búsqueda de palabras escondidas y una bóveda final con boarding pass. Mobile-first, un solo `index.html`, sin frameworks.

## 🔗 Link

- **En vivo:** https://tommyhanono.github.io/mientras-no-estoy/
- **Preview (desbloquea todo):** https://tommyhanono.github.io/mientras-no-estoy/?debug=1

## Estructura

```
index.html          → toda la app (HTML + CSS + JS embebidos)
photos/             → dia2.jpg, dia9.jpg, tommy.jpg, rompecabezas.jpg
audio/cancion.m4a   → nuestra canción (Día 6)
video/              → cumple.mp4 y final.mp4 (se agregan después — ver ADD_CONTENT.md)
ADD_CONTENT.md      → cómo subir los videos y actualizar el sitio
```

## Detalles

- Se desbloquea un día por medianoche (hora de Panamá). Los días pasados quedan re-abribles.
- La clave de la bóveda se arma con 13 palabras, una por día: *Hola Tommy Te Amo Mucho Quiero Que Me Muerdas Y Me Hagas Cosquillas*.
- Progreso guardado en `localStorage`.
