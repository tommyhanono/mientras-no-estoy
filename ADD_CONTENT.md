# Cómo agregar los videos (y actualizar el sitio)

Este calendario ya está 100% funcional. Faltan **solo 2 videos** que se agregan después. Mientras no estén, el sitio muestra un placeholder bonito ("tommy está preparando algo... 👀") — nunca se ve roto.

## Los 2 videos pendientes

| Archivo | Dónde aparece | Cuándo subirlo |
|---|---|---|
| `video/cumple.mp4` | Día 3 (cumpleaños), debajo de la carta | **antes del 8 de julio 2026** |
| `video/final.mp4` | Día 14 (la bóveda), primer paso del final | **antes del 19 de julio 2026** |

**Formato recomendado:** MP4 (H.264 + AAC), vertical, máx ~30–40 MB para que cargue rápido en el iPhone de Vicky.
Si tu video es `.mov` (grabado con iPhone), conviértelo con:

```bash
# desde ~/mientras-no-estoy
ffmpeg -i /ruta/al/video.mov -vf "scale='min(1080,iw)':-2" -c:v libx264 -crf 24 -c:a aac -movflags +faststart video/cumple.mp4
```

(cambia `cumple.mp4` por `final.mp4` según corresponda)

## Subir un video (o cualquier cambio)

```bash
cd ~/mientras-no-estoy

# 1) copia el video a la carpeta correcta
cp /ruta/al/video.mp4 video/cumple.mp4      # o video/final.mp4

# 2) súbelo a GitHub (se publica solo en 1-2 min)
git add video/cumple.mp4
git commit -m "Agregar video del cumpleaños"
git push
```

GitHub Pages se actualiza automáticamente. Espera 1–2 minutos y recarga la página.

## Probar todo antes de mandárselo a Vicky

Abre el sitio con `?debug=1` al final del URL:

```
https://tommyhanono.github.io/mientras-no-estoy/?debug=1
```

Con `?debug=1`:
- Se desbloquean **todos los días** (para probar sin esperar).
- Aparece una etiqueta roja "DEBUG" abajo a la derecha.

Recorre los 14 días, revisa que las palabras se junten en el **Diario de Pistas**, y prueba la **Bóveda** (Día 14) escribiendo la clave completa:

> `Hola Tommy Te Amo Mucho Quiero Que Me Muerdas Y Me Hagas Cosquillas`

⚠️ **Importante:** cuando termines de probar, **borra el `?debug=1`** antes de mandarle el link a ella. El link que le mandas debe ser el limpio:

```
https://tommyhanono.github.io/mientras-no-estoy/
```

Así ella sí tiene que pasar la pantalla de bloqueo y esperar cada día 😌

## Notas técnicas

- Todo el progreso de Vicky (días abiertos, palabras, extrañómetro, respuestas) se guarda en `localStorage` de **su** teléfono. No se comparte entre dispositivos.
- Los días se desbloquean a **medianoche hora de Panamá**. Los días pasados quedan re-abribles.
- Las respuestas de "Pregunta del día" y misiones abren WhatsApp hacia tu número (`50766818669`) con el texto ya escrito.
