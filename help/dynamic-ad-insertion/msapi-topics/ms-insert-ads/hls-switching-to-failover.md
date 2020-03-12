---
description: La pila HLS de Apple admite el cambio a flujos de failover/backup si no puede recuperar ningún flujo del conjunto principal. Para los dispositivos Apple HLS, para facilitar la conmutación por error, puede indicar al servidor de manifiesto que trate los flujos principales y de conmutación por error identificados en la lista de reproducción maestra como conjuntos desunidos (con sus propios UUID).
seo-description: La pila HLS de Apple admite el cambio a flujos de failover/backup si no puede recuperar ningún flujo del conjunto principal. Para los dispositivos Apple HLS, para facilitar la conmutación por error, puede indicar al servidor de manifiesto que trate los flujos principales y de conmutación por error identificados en la lista de reproducción maestra como conjuntos desunidos (con sus propios UUID).
seo-title: Facilitación del cambio del reproductor HLS a flujos de failover/backup
title: Facilitación del cambio del reproductor HLS a flujos de failover/backup
uuid: 2fea8a51-e4cb-4fc9-82d5-6305a1d96603
translation-type: tm+mt
source-git-commit: 6863b63c7fa0068c3c5060fb946515c6cc5e3bff

---


# Facilitación del cambio del reproductor HLS a flujos de failover/backup {#facilitating-hls-player-switching-to-failover-backup-streams}

La pila HLS de Apple admite el cambio a flujos de failover/backup si no puede recuperar ningún flujo del conjunto principal. Para los dispositivos Apple HLS, para facilitar la conmutación por error, puede indicar al servidor de manifiesto que trate los flujos principales y de conmutación por error identificados en la lista de reproducción maestra como conjuntos desunidos (con sus propios UUID).

Para facilitar el cambio a flujos de conmutación por error o de copia de seguridad en dispositivos Apple HLS, puede especificar el `ptfailover` parámetro en la URL de Bootstrap. Si proporciona este parámetro, el servidor de manifiesto creará sesiones de reproducción independientes (que determinan las publicidades que se vinculan) para cada conjunto de conmutación por error.

## Detalles

Cómo gestiona SSAI el cambio de HLS a failover/backup cuando se incluye `ptfailover=true` en la solicitud de Bootstrap:

* Cuando una lista de reproducción maestra contiene conjuntos primarios y de copia de seguridad:

   * El servidor de manifiesto identifica las direcciones URL de flujo AV para distintos conjuntos de conmutación por error mediante el atributo y el orden de análisis de las direcciones URL de flujo AV. `BANDWIDTH` Crea sesiones de reproducción internas independientes (identificadas por UUID independientes) y direcciones URL de flujo que apuntan a servidores de manifiesto con los distintos UUID que identifican diferentes sesiones de reproducción.
   * El servidor de manifiesto identifica las direcciones URL de flujo de I-Frame para diferentes conjuntos de conmutación por error utilizando el `RESOLUTION` atributo correspondiente y el orden de análisis de las direcciones URL de flujo de I-Frame. SSAI utiliza los UUID que identifican los flujos AV asociados para las URL de flujo de I-Frame que apuntan a SSAI.
   * Para esta función, el servidor de manifiesto solo admite `EXT-X-MEDIA` grupos sin atributos URI en la lista de reproducción maestra.
   * El servidor de manifiesto detecta una respuesta de error 404 de una CDN con un `X-Object-Too-Old: true` encabezado y conserva el código de estado y el encabezado al enviar esa respuesta al reproductor.

* Las publicidades previas al lanzamiento solo se agregan al conjunto principal; están completamente desactivados en los conjuntos de conmutación por error para evitar anuncios previos erróneos o duplicados cuando el reproductor cambia a flujos de conmutación por error.

