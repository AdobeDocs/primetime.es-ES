---
description: Los editores pueden crear reproductores de vídeo compatibles con HLS que trabajen con los flujos de trabajo de seguimiento de anuncios del lado del cliente del manifiesto Primetime. Las interfaces al servidor de manifiesto para los casos de flujo en directo y vídeo a petición (VOD) son ligeramente diferentes.
seo-description: Los editores pueden crear reproductores de vídeo compatibles con HLS que trabajen con los flujos de trabajo de seguimiento de anuncios del lado del cliente del manifiesto Primetime. Las interfaces al servidor de manifiesto para los casos de flujo en directo y vídeo a petición (VOD) son ligeramente diferentes.
seo-title: Información general sobre el seguimiento del cliente que no es TVSDK
title: Información general sobre el seguimiento del cliente que no es TVSDK
uuid: fb23be01-3327-443d-82c4-fb0993e7fec1
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 0%

---


# Información general sobre el seguimiento del cliente que no es TVSDK {#overview-of-non-tvsdk-client-side-tracking}

Los editores pueden crear reproductores de vídeo compatibles con HLS que trabajen con los flujos de trabajo de seguimiento de anuncios del lado del cliente del manifiesto Primetime. Las interfaces al servidor de manifiesto para los casos de flujo en directo y vídeo a petición (VOD) son ligeramente diferentes.

El servidor de manifiesto proporciona una API para permitir que los reproductores personalizados soliciten las siguientes direcciones URL, que pueden utilizar para informar sobre eventos de seguimiento de anuncios:

* Impresión de publicidad
* Cuartilo publicitario
* Progreso del pod de publicidad
* Progreso del pod de contenido

La API de servidor de manifiesto supone que cualquier reproductor de vídeo que lo utilice cumple los requisitos mínimos. Consulte [Requisitos del reproductor de vídeo](../../msapi-topics/ms-player-req.md) para obtener más información.

## Flujo de trabajo de seguimiento del lado del cliente {#section_cst_flow}

![](assets/pt_ssai_notvsdk_csat_ai-workflow.png)

1. Player obtiene una URL de servidor de manifiesto del editor.
1. Player anexa parámetros de consulta específicos a sus requisitos de inserción de publicidad y envía una solicitud de GET HTTP a la URL del Bootstrap resultante. La dirección URL del Bootstrap tiene la siguiente sintaxis:

   ```
   http{s}://{manifest-server:port}/auditude/variant/{PublisherAssetID}/{urlSafeBase64({Content URL})}.m3u8?{query parameters}
   
   For example:
   https://manifest.auditude.com/auditude/variant/
   7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/aHR0cDovL3B0ZGVtb3MuY29tL3ZpZGVvcy90b3NoZHVuZW5jcnlwdGVkL2hscy90ZXN0Mi5tM3U4.m3u8?
   u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2&__sid__=docExample02
   ```

   La dirección URL incluye los elementos descritos en [Enviar un comando al servidor de manifiesto](../../msapi-topics/ms-getting-started/ms-sending-cmd.md).

1. El servidor de manifiesto establece una sesión para ese reproductor y genera un ID de sesión único. Crea una nueva URL de lista de reproducción M3U8 de variante, que vuelve al reproductor como una respuesta JSON. El JSON tiene la siguiente sintaxis:

   ```
   {
    "Master-M3U8": "https://{manifest-server:port}/auditude/variant/{PublisherAssetID}/{SessionID}/
       {urlSafeBase64(content URL)}.m3u8?u={Asset ID}&z={Zone ID}&pttrackingmode=simple&pttrackingversion=v2
       &{Any other query parameters}"
   }
   
   For example:
   https://pcor3.manifest.auditude.com/auditude/variant/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3B0ZGVtb3MuY29tL3ZpZGVvcy90b3NoZHVuZW5jcnlwdGVkL2hscy90ZXN0Mi5tM3U4.3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   ```

1. El reproductor utiliza la URL de la respuesta JSON para solicitar la nueva variante M3U8 de la lista de reproducción maestra del servidor de manifiesto.
1. El servidor de manifiesto devuelve una nueva variante M3U8 que contiene direcciones URL de listas de reproducción de nivel de flujo con una sintaxis similar a la siguiente:

   ```
   http{s}://{manifest-server:port}/auditude/{live|vod}/{PublisherAssetID}/
     {rendition}/{groupID}/{urlSafeBase64(bit rate stream URL)}.m3u8?u={Ad Request Id}&z={Ad Zone Id}&{Any other query parameters}
   
   For example:
   #EXTM3U
   #EXT-X-VERSION:5
   #EXT-X-MEDIA:TYPE=SUBTITLES,GROUP-ID="subs",NAME="English",AUTOSELECT=YES,DEFAULT=YES,FORCED=NO,LANGUAGE="eng",URI="https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/webvtt/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvd2VidnR0L1RPUy1lbjIubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2"
   #EXT-X-STREAM-INF:BANDWIDTH=10000000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/10000/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvMTAwMDAvdG9jXzEwMDAwLm0zdTg.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=1300000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/1300/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvMTMwMC90b2NfMTMwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=3400000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/3400/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvMzQwMC90b2NfMzQwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=2100000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/2100/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvMjEwMC90b2NfMjEwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=800000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/800/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvODAwL3RvY184MDAubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=5000000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/5000/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNTAwMC90b2NfNTAwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=7500000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/7500/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNzUwMC90b2NfNzUwMC5tM3U4.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   #EXT-X-STREAM-INF:BANDWIDTH=500000,SUBTITLES="subs"
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/500/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNTAwL3RvY181MDAubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   ```

1. El reproductor selecciona la URL de manifiesto de nivel de flujo y velocidad de bits única adecuada para reproducir el contenido con una publicidad. Por ejemplo:

   ```
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/500/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNTAwL3RvY181MDAubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d&z=173475&pttrackingmode=simple&pttrackingversion=v2
   ```

1. El servidor de manifiesto devuelve un manifiesto de nivel de flujo que contiene vínculos al contenido y a los vínculos de segmentos de TS de anuncio. Por ejemplo:

   ```
      #EXTM3U
   #EXT-X-VERSION:3
   #EXT-X-TARGETDURATION:8
   #EXT-X-PLAYLIST-TYPE:VOD
   
   #EXT-X-DISCONTINUITY
   #EXTINF:8,
   https://primetime-a.akamaihd.net/assets/repackage/production/zen/195/10516675/2ac89785ee8df17a31b2594c61f6921e-300k-00001.ts
   #EXTINF:7,
   https://primetime-a.akamaihd.net/assets/repackage/production/zen/195/10516675/2ac89785ee8df17a31b2594c61f6921e-300k-00002.ts
   
   #EXT-X-DISCONTINUITY
   #EXTINF:4,
   https://www.ptdemos.com/videos/toshdunencrypted/hls/500/toc_500.0.ts
   #EXTINF:4,
   https://www.ptdemos.com/videos/toshdunencrypted/hls/500/toc_500.4000.ts
   #EXTINF:4.833,
   https://www.ptdemos.com/videos/toshdunencrypted/hls/500/toc_500.8000.ts   
   ```

   >[!NOTE]
   >
   >El reproductor selecciona la URL de la lista de reproducción de nivel de flujo para obtener el flujo de contenido. El servidor de manifiesto recupera la lista de reproducción original de la CDN. Algunos codificadores pueden introducir detalles adicionales en el atributo de título `#EXTINF`, por ejemplo:
   >
   >
   ```
   >#EXTINF:6.006,LTC=2017-08-23T13:25:47+00:00
   >```

   Dado que el servidor de manifiesto no puede inferir el significado de atributos no estándar para modificarlos en la lista de reproducción con vinculación de publicidad, el servidor de manifiesto elimina todos los atributos adicionales más allá de la información de duración de esta etiqueta. Consulte la entrada [EXTINF](https://tools.ietf.org/html/rfc8216#section-4.3.2.1) en la especificación HLS para obtener más información.


1. Para solicitar información de seguimiento, el reproductor anexa el parámetro de consulta `pttrackingposition` con cualquier valor alfanumérico a la URL de la lista de reproducción de nivel de flujo para la velocidad de bits seleccionada. Por ejemplo:

   ```
   https://pcor3.manifest.auditude.com/auditude/vod/7LTc86_kMUDFcCjoH9X7K_2auwb_gnWM/500/f958bef8-9158-43cc-80b9-4b15417b7895/aHR0cDovL3d3dy5wdGRlbW9zLmNvbS92aWRlb3MvdG9zaGR1bmVuY3J5cHRlZC9obHMvNTAwL3RvY181MDAubTN1OA.m3u8?u=9a2893fd893cab27da24059ff034b78d
   &z=173475&pttrackingmode=simple&pttrackingversion=v2&pttrackingposition=1
   ```

1. El servidor de manifiesto devuelve el archivo de lista de reproducción rellenado con un objeto [JSON](../../msapi-topics/ms-list-file-formats/notvsdk-csat-sidecar.md) o [VMAP](../../msapi-topics/ms-list-file-formats/notvsdk-csat-vmap.md) que contiene los datos de seguimiento de publicidad para el archivo m3u8 de nivel de flujo solicitado actualmente.

   >[!NOTE]
   >
   >El servidor de manifiesto solo generará objetos de seguimiento de publicidad si se insertaron publicidades en la lista de reproducción de nivel de flujo actualmente solicitada. Si el reproductor está reproduciendo una lista de reproducción que no contiene anuncios insertados, el servidor de manifiesto devuelve un estado HTTP 201 para la solicitud de la lista de reproducción de seguimiento de publicidad. Si el reproductor realiza la solicitud de seguimiento de anuncios para un flujo que no se está reproduciendo, el servidor de manifiesto devolverá un estado HTTP 500. Por ejemplo, si la solicitud de reproducción actual es para 500.m3u8, el servidor de manifiesto devuelve un JSON|VMAP en el 500.m3u8 para la solicitud de seguimiento de publicidad. Sin embargo, si posteriormente el reproductor cambia los flujos para reproducir el 800.m3u8, la información del seguimiento de anuncios en el 500.m3u8 se torna no válida, lo que provoca un error 404.

   >[!NOTE]
   >
   >El servidor de manifiesto genera el objeto de seguimiento de publicidad basado en el valor `pttrackingversion` en la dirección URL del Bootstrap. Si el `pttrackingversion` se omite o tiene un valor no válido, el servidor de manifiesto rellenará automáticamente la información de seguimiento de publicidad en las etiquetas `#EXT-X-MARKER` de cada lista de reproducción de nivel de flujo solicitada. Consulte [para obtener más información](../../msapi-topics/ms-at-effectiveness/ms-api-playlists.md).

1. El reproductor solicita cada dirección URL de seguimiento de publicidad para cada evento de seguimiento de publicidad en el momento adecuado.

>[!NOTE]
>
>Para los flujos en directo, el reproductor debe repetir los pasos 6 a 10, ya que el empaquetador actualiza constantemente la lista de reproducción durante todo el evento en directo.

A medida que se reproduce el vídeo, el reproductor debe rastrear la posición del cursor de reproducción y utilizar esta posición junto con las URL de seguimiento que recibió de Primetime y la inserción. Las direcciones URL de seguimiento se agrupan por desplazamiento de tiempo desde el comienzo de la reproducción. Por cada desplazamiento de tiempo, hay una dirección URL para cada sistema de publicidad a la cual enviar la información de seguimiento. Los detalles adicionales del formato difieren entre vídeo en directo y vídeo a petición.
