---
title: Facilitar el cambio del reproductor HLS a flujos de failover/backup
description: La pila HLS de Apple admite el cambio a flujos de conmutación por error/copia de seguridad si no puede recuperar ningún flujo del conjunto principal. En el caso de dispositivos HLS de Apple, para facilitar la conmutación por error, puede indicar al servidor de manifiesto que trate los flujos de conmutación por error principales y los identificados en la lista de reproducción maestra como conjuntos separados (con sus propios UUID).
exl-id: 58c7a490-403f-41b2-bdbd-6f93e27083b0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# Facilitar el cambio del reproductor HLS a flujos de failover/backup {#facilitating-hls-player-switching-to-failover-backup-streams}

La pila HLS de Apple admite el cambio a flujos de conmutación por error/copia de seguridad si no puede recuperar ningún flujo del conjunto principal. En el caso de dispositivos HLS de Apple, para facilitar la conmutación por error, puede indicar al servidor de manifiesto que trate los flujos de conmutación por error principales y los identificados en la lista de reproducción maestra como conjuntos separados (con sus propios UUID).

Para facilitar el cambio a flujos de conmutación por error o de copia de seguridad en dispositivos HLS de Apple, puede especificar el `ptfailover` en la URL del Bootstrap. Si proporciona este parámetro, el servidor de manifiesto creará sesiones de reproducción independientes (que determinan los anuncios vinculados) para cada conjunto de conmutación por error.

## Detalles

Cómo administra SSAI el cambio de HLS a failover/backup cuando incluye `ptfailover=true` en la solicitud del Bootstrap:

* Cuando una lista de reproducción principal contiene conjuntos principales y de copia de seguridad:

   * El servidor de manifiesto identifica las direcciones URL de secuencias AV para diferentes conjuntos de conmutación por error mediante el `BANDWIDTH` y el orden de análisis de las direcciones URL de las secuencias audiovisuales. Crea sesiones de reproducción interna independientes (identificadas por UUID independientes) y direcciones URL de flujo que apuntan a servidores de manifiesto con los distintos UUID que identifican sesiones de reproducción diferentes.
   * El servidor de manifiesto identifica las direcciones URL de flujo de I-Frame para diferentes conjuntos de conmutación por error mediante el `RESOLUTION` y el orden de análisis de las URL de flujo de I-Frame. SSAI utiliza los UUID que identifican los flujos AV asociados para las URL de flujo de I-Frame que apuntan a SSAI.
   * Para esta función, el servidor de manifiesto solo admite `EXT-X-MEDIA` grupos sin atributos URI en la lista de reproducción principal.
   * El servidor de manifiesto detecta una respuesta de error 404 de una CDN con un `X-Object-Too-Old: true` y conserva el código de estado y el encabezado al enviar esa respuesta al reproductor.

* Los anuncios previos a la emisión solo se añaden al conjunto principal; se desactivan por completo en los conjuntos de failover para evitar anuncios previos a la emisión erróneos o duplicados cuando el reproductor cambia a flujos de failover.
