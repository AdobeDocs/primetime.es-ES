---
description: Utilice los parámetros opcionales de consulta pttrackingmode, pttrackingversion y pttrackingposition para obtener las direcciones URL a las que enviar información de seguimiento de anuncios sobre el vídeo actual. Las respuestas varían con la versión de seguimiento y si el flujo de vídeo está activo o bajo demanda (VOD).
title: API para que los reproductores interactúen con el servidor de manifiesto
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---


# API para que los reproductores interactúen con el servidor de manifiesto {#api-for-players-to-interact-with-the-manifest-server}

Utilice los parámetros de consulta opcionales `pttrackingmode`, `pttrackingversion` y `pttrackingposition` para obtener las direcciones URL a las que enviar información de seguimiento de anuncios sobre el vídeo actual. Las respuestas varían con la versión de seguimiento y si el flujo de vídeo está activo o bajo demanda (VOD).

## Parámetros de consulta {#query-parameters}

**pttrackingmode**

Ejemplo: `pttrackingmode=simple`
Si se especifica simple, se indica al servidor de manifiesto que desea realizar el seguimiento de la información.
Especifíquelo en una solicitud para recuperar el M3U8 antes de solicitar la información de seguimiento. Cuando no la especifique, el servidor de manifiesto devolverá información de seguimiento en las etiquetas #EXT-X-MARKER.
O bien, si especifica un valor válido que no sea simple, se invoca el seguimiento del lado del servidor.

**pttrackingversion**

Ejemplo: `pttrackingversion=v2`
Este parámetro indica al servidor de manifiesto qué formato utilizar para devolver información de seguimiento (consulte [Formatos de archivo](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md)).
Especifíquelo en una solicitud para recuperar el M3U8 antes de solicitar información de seguimiento. Cuando no la especifique, o especifique un valor no válido, el servidor de manifiesto utilizará el v1.

**pttrackingposition**

Ejemplo: `pttrackingposition`
Este parámetro indica al servidor de manifiesto que devuelva información de seguimiento del vídeo como un objeto JSON o VMAP en el archivo M3U8. El servidor de manifiesto ignora el valor especificado y envía toda la información de seguimiento que tiene para esa sesión. Si no se pasa ningún valor, el servidor de manifiesto devuelve el archivo M3U8 solicitado.
