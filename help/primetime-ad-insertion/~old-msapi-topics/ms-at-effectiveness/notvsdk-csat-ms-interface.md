---
description: Utilice los parámetros de consulta opcionales pttrackingmode, pttrackingversion y pttrackingposition para obtener direcciones URL a las que enviar información de seguimiento de anuncios acerca del vídeo actual. Las respuestas varían con la versión de seguimiento y si el flujo de vídeo está activo o bajo demanda (VOD).
title: API para que los reproductores interactúen con el servidor de manifiesto
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---


# API para que los reproductores interactúen con el servidor de manifiesto {#api-for-players-to-interact-with-the-manifest-server}

Utilice el opcional `pttrackingmode`, `pttrackingversion`, y `pttrackingposition` parámetros de consulta para obtener direcciones URL a las que enviar información de seguimiento de anuncios acerca del vídeo actual. Las respuestas varían con la versión de seguimiento y si el flujo de vídeo está activo o bajo demanda (VOD).

## Parámetros de consulta {#query-parameters}

**pttrackingmode**

Ejemplo: `pttrackingmode=simple`
Especificar simple indica al servidor de manifiesto que desea obtener información de seguimiento.
Especifíquela en una solicitud para recuperar el M3U8 antes de solicitar información de seguimiento. Si no la especifica, el servidor de manifiesto devuelve información de seguimiento en las etiquetas #EXT-X-MARKER.
O bien, si especifica un valor válido que no sea simple, se invocará el seguimiento del lado del servidor.

**pttrackingversion**

Ejemplo: `pttrackingversion=v2`
Este parámetro indica al servidor de manifiesto qué formato utilizar para devolver la información de seguimiento (consulte [Formatos de archivo](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md)).
Especifíquelo en una solicitud para recuperar el M3U8 antes de solicitar información de seguimiento. Cuando no lo especifique, o especifique un valor no válido, el servidor de manifiesto utilizará v1.

**pttrackingposition**

Ejemplo: `pttrackingposition`
Este parámetro indica al servidor de manifiesto que devuelva la información de seguimiento del vídeo como un objeto JSON o VMAP en el archivo M3U8. El servidor de manifiesto ignora el valor especificado y envía toda la información de seguimiento que tiene para esa sesión. Si no se pasa ningún valor, el servidor de manifiesto devolverá el archivo M3U8 solicitado.
