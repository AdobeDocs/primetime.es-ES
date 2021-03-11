---
description: La pila HLS de Apple admite el cambio a flujos de failover/backup si no puede recuperar ningún flujo del conjunto principal. Para los dispositivos HLS de Apple, para facilitar la conmutación por error, puede indicar al servidor de manifiesto que trate los flujos principales y de conmutación por error identificados en la lista de reproducción maestra como conjuntos separados (con sus propios UUID).
title: Facilitación del cambio del reproductor HLS a flujos de failover/backup
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---


# Facilitación del cambio del reproductor HLS a flujos de failover/backup {#facilitating-hls-player-switching-to-failover-backup-streams}

La pila HLS de Apple admite el cambio a flujos de failover/backup si no puede recuperar ningún flujo del conjunto principal. Para los dispositivos HLS de Apple, para facilitar la conmutación por error, puede indicar al servidor de manifiesto que trate los flujos principales y de conmutación por error identificados en la lista de reproducción maestra como conjuntos separados (con sus propios UUID).

Para facilitar el cambio a flujos de conmutación por error o de copia de seguridad en dispositivos HLS de Apple, puede especificar el parámetro `ptfailover` en la dirección URL del Bootstrap. Si proporciona este parámetro, el servidor de manifiesto creará sesiones de reproducción independientes (que determinan los anuncios vinculados) para cada conjunto de conmutación por error.

## Detalles

Cómo SSAI administra el cambio HLS a failover/backup cuando se incluye `ptfailover=true` en la solicitud del Bootstrap:

* Cuando una lista de reproducción maestra contiene conjuntos primarios y de copia de seguridad:

   * El servidor de manifiesto identifica las URL de flujo AV para diferentes conjuntos de conmutación por error utilizando el atributo `BANDWIDTH` y el orden de análisis de las URL de flujo AV. Crea sesiones de reproducción internas independientes (identificadas mediante UUID independientes) y crea direcciones URL de flujo que apuntan a servidores de manifiesto con los diferentes UUID que identifican diferentes sesiones de reproducción.
   * El servidor de manifiesto identifica las URL de flujo de I-Frame para diferentes conjuntos de conmutación por error utilizando el atributo `RESOLUTION` correspondiente y el orden de análisis de las URL de flujo de I-Frame. SSAI utiliza los UUID que identifican los flujos AV asociados para URL de flujo de I-Frame que apuntan a SSAI.
   * Para esta función, el servidor de manifiestos solo admite grupos `EXT-X-MEDIA` sin atributos de URI en la lista de reproducción maestra.
   * El servidor de manifiestos detecta una respuesta de error 404 de una CDN con un encabezado `X-Object-Too-Old: true` y conserva el código de estado y el encabezado al enviar esa respuesta al reproductor.

* Los anuncios previos a la emisión solo se agregan al conjunto principal; están completamente desactivados en los conjuntos de conmutación por error para evitar anuncios previos a la emisión erróneos o duplicados cuando el reproductor cambia a flujos de conmutación por error.

