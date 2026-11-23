# GTA 6 Clip Studio

Aplicación web estática optimizada para Safari en iPhone. El proyecto reemplaza por completo la interfaz anterior y puede publicarse con GitHub Pages.

## Funciones locales

- Selección de vídeos desde Archivos o Fotos mediante `<input accept="video/*">`.
- Reproducción y selección de inicio/final.
- Búsqueda heurística local de momentos con cambios de movimiento.
- Conversión visual a 9:16 mediante canvas.
- Textos, subtítulos manuales y efectos localmente.
- Exportación mediante `MediaRecorder` y `canvas.captureStream`, con resultado MP4 cuando Safari informa soporte H.264/AAC.
- Compartir mediante Web Share API y archivos.

## Importante sobre Safari y iPhone

MediaRecorder y `canvas.captureStream()` dependen de la versión de iOS/Safari. El archivo fuente debe ser compatible con el decodificador del iPhone: MP4 H.264/AAC es la opción más estable. Los recortes están limitados a 90 segundos para reducir el riesgo de quedarse sin memoria.

## IA y subtítulos

La aplicación no simula IA ni transcribe dentro del navegador. El análisis externo es opcional y se activa configurando una URL HTTPS propia. Para producción se recomienda no meter una clave privada en el navegador: crea un endpoint autenticado que expida solicitudes autorizadas o una sesión temporal.

El endpoint debe aceptar:

- `POST` multipart/form-data.
- Campos `file`, `start`, `end`, `language=es` y `purpose=highlights|captions`.
- Cabecera opcional `Authorization: Bearer <clave>`.

Respuesta JSON de highlights:

```json
{
  "highlights": [
    { "start": 12.4, "end": 32.4, "score": 0.92 }
  ]
}
```

Respuesta JSON de subtítulos:

```json
{
  "captions": [
    { "start": 0, "end": 3.2, "text": "Texto reconocido" }
  ]
}
```

Los servicios recomendados son un backend propio con Whisper/faster-whisper para transcripción y un modelo o análisis de escena para highlights. El servidor debe devolver tiempos relativos al clip seleccionado y aplicar límite de tamaño, CORS, autenticación y eliminación temporal del archivo.

## Publicación

1. GitHub Pages puede publicar la rama `main` en la raíz.
2. Usa HTTPS para que Web Share y las APIs externas funcionen correctamente.
3. No uses YouTube como entrada: los navegadores no pueden descargar/recombinar vídeos de YouTube de forma legítima ni estable sin una integración de servidor con permisos adecuados.

## Marca

Proyecto independiente y sin afiliación con Rockstar Games, Take-Two Interactive o YouTube.
