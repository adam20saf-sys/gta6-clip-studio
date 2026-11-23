# GTA 6 Clip Studio

Aplicación web estática optimizada para Safari en iPhone.

## Verificación incluida

- Subida desde Archivos/Fotos mediante `accept="video/*"`.
- Recorte manual y heurística local de movimiento.
- Formato vertical 1080×1920.
- Texto y tres efectos visuales.
- Exportación con `MediaRecorder` y pista de audio de `MediaStreamDestination`.
- Compartir mediante Web Share API, con descarga como alternativa.
- Límites de 2 GB en el archivo y 90 segundos por exportación.

## IA y subtítulos

El análisis automático externo es opcional. Debe configurarse una URL HTTPS propia. El navegador envía el vídeo mediante POST multipart. El servidor debe validar el tamaño, limitar peticiones, habilitar CORS para el origen de GitHub Pages y eliminar los archivos temporales.

Contrato esperado:

- Campos: `file`, `start`, `end`, `language=es`, `purpose=highlights|captions`.
- Highlights: `{ "highlights": [{ "start": 12.4, "end": 32.4 }] }`.
- Subtítulos: `{ "captions": [{ "start": 0, "end": 3.2, "text": "Texto" }] }`.

Las marcas de tiempo deben ser relativas al recorte solicitado. En producción no incluyas claves privadas en el archivo; usa autenticación temporal o un proxy protegido.

## Compatibilidad

Usa MP4 con H.264/AAC. Safari determina el `mimeType` admitido con `MediaRecorder.isTypeSupported()`. Si Safari no ofrece MP4, solo queda actualizar iOS/Safari o usar FFmpeg en un servidor externo. La aplicación no descarga vídeos de YouTube ni simula una función IA inexistente.

## Publicación

GitHub Pages debe servir `index.html` desde la rama `main` por HTTPS.
