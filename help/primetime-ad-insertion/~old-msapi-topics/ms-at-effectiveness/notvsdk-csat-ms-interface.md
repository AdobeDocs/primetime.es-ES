---
description: Utilice los parámetros opcionales de consulta pttrackingmode, pttrackingversion y pttrackingposition para obtener las direcciones URL a las que enviar información de seguimiento de anuncios sobre el vídeo actual. Las respuestas varían según la versión de seguimiento y si el flujo de vídeo está activo o bajo demanda (VOD).
seo-description: Utilice los parámetros opcionales de consulta pttrackingmode, pttrackingversion y pttrackingposition para obtener las direcciones URL a las que enviar información de seguimiento de anuncios sobre el vídeo actual. Las respuestas varían según la versión de seguimiento y si el flujo de vídeo está activo o bajo demanda (VOD).
seo-title: API para que los reproductores interactúen con el servidor de manifiesto
title: API para que los reproductores interactúen con el servidor de manifiesto
uuid: ab7a19e7-6c28-4960-a56b-3b33c525e6b3
translation-type: tm+mt
source-git-commit: e1e33d3ac0aad44859cd49566331524da72ac7e4
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---


# API para que los reproductores interactúen con el servidor de manifiesto {#api-for-players-to-interact-with-the-manifest-server}

Utilice los parámetros de consulta `pttrackingmode`, `pttrackingversion` y `pttrackingposition` opcionales para obtener direcciones URL a las que enviar información de seguimiento de publicidad sobre el vídeo actual. Las respuestas varían según la versión de seguimiento y si el flujo de vídeo está activo o bajo demanda (VOD).

## Parámetros de consulta {#query-parameters}

**pttrackingmode**

Ejemplo: `pttrackingmode=simple`
Si se especifica simple, se indica al servidor de manifiesto que se desea realizar el seguimiento de la información.
Especifíquelo en una solicitud para recuperar la M3U8 antes de solicitar la información de seguimiento.Cuando no la especifica, el servidor de manifiesto devuelve la información de seguimiento en las etiquetas #EXT-X-MARKER.
O bien, si especifica un valor válido que no sea simple, se invoca el seguimiento del lado del servidor.

**pttrackingversion**

Ejemplo: `pttrackingversion=v2`
Este parámetro indica al servidor de manifiesto qué formato utilizar para devolver información de seguimiento (consulte [Formatos de archivo](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md)).
Especifíquelo en una solicitud para recuperar el M3U8 antes de solicitar la información de seguimiento.Cuando no la especifica, o especifique un valor no válido, el servidor de manifiesto utiliza v1.

**pttrackingposition**

Ejemplo: `pttrackingposition`
Este parámetro indica al servidor de manifiesto que devuelva información de seguimiento del vídeo como un objeto JSON o VMAP en el archivo M3U8. El servidor de manifiesto omite el valor especificado y envía toda la información de seguimiento que tiene para esa sesión. Si no se pasa ningún valor, manifest server devuelve el archivo M3U8 solicitado.