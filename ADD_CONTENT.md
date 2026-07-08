# Cómo agregar los videos (y actualizar el sitio)

Este calendario ya está 100% funcional. El video del cumpleaños (Día 3) **ya está subido** ✅. Falta **solo 1 video** (el del Día 14), que se agrega después. Mientras no esté, el sitio muestra un placeholder bonito ("tommy dejó algo aquí... cargando 👀") — nunca se ve roto.

## Video pendiente

| Archivo | Dónde aparece | Cuándo subirlo |
|---|---|---|
| ~~`video/cumple.mp4`~~ | ~~Día 3 (cumpleaños)~~ | ✅ **LISTO** (subido) |
| `video/final.mp4` | Día 14 (la bóveda), primer paso del final | **antes del 19 de julio 2026** |

**Formato recomendado:** MP4 (H.264 + AAC), vertical, máx ~30–40 MB para que cargue rápido en el iPhone de Vicky.

Si tu video es `.MOV` de iPhone, casi seguro es **HEVC 10-bit HDR** (se vería lavado/gris en la web sin convertir bien). Usa exactamente este comando — es el mismo que usé para el video del cumple (convierte HDR→SDR con tono correcto, comprime, y arregla la orientación):

```bash
# desde ~/mientras-no-estoy
ffmpeg -y -i /ruta/al/video.MOV \
  -map 0:0 -map 0:1 \
  -vf "zscale=t=linear:npl=100,format=gbrpf32le,zscale=p=bt709,tonemap=tonemap=hable:desat=0,zscale=t=bt709:m=bt709:r=tv,format=yuv420p" \
  -c:v libx264 -crf 25 -preset medium -pix_fmt yuv420p -movflags +faststart \
  -c:a aac -b:a 128k -ac 2 \
  video/final.mp4
```

**Poster (opcional pero recomendado):** para que se vea un thumbnail bonito en vez de una caja negra, saca un frame:

```bash
ffmpeg -y -ss 0.6 -i video/final.mp4 -frames:v 1 -vf "scale=720:-2" -q:v 3 video/final_poster.jpg
```

...y avísame para conectarlo en el Día 14 (o dime y lo dejo listo yo). El del cumple ya tiene su poster.

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
