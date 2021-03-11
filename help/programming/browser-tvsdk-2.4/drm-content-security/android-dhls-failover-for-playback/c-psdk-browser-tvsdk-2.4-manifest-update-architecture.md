---
description: A continuación se proporcionan información y ejemplos sobre cómo el TVSDK del explorador admite los manifiestos maestros actualizados.
title: Arquitectura de actualización de manifiesto maestro activo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 1%

---


# Arquitectura de actualización de manifiesto maestro en vivo{#live-master-manifest-update-architecture}

A continuación se proporcionan información y ejemplos sobre cómo el TVSDK del explorador admite los manifiestos maestros actualizados.

De forma predeterminada, esta función está desactivada. Si la aplicación la activa estableciendo una frecuencia de actualización en minutos, se producirán los siguientes pasos después de cada intervalo de actualización:

1. El SDK del explorador comprueba la hora y la etiqueta de la última modificación del manifiesto maestro para determinar si el archivo se ha actualizado.

   Si tanto la hora como la etiqueta han cambiado, el archivo se considera modificado.
1. El SDK del explorador analiza y analiza el nuevo manifiesto y adopta las medidas adecuadas en función de la naturaleza de la actualización.
1. Si la velocidad de bits de reproducción actual coincide con la velocidad de bits del manifiesto modificado, el SDK de TVSDK del explorador cambia al nuevo perfil.

   El nuevo perfil podría ser de un servidor diferente o del mismo servidor, a la misma velocidad de bits. En este caso, la transición es suave.
1. Si la velocidad de bits de reproducción actual ya no está presente en el nuevo manifiesto, el TVSDK del explorador intenta encontrar una tasa de bits en el perfil actual que también existe en el nuevo manifiesto.

   * Si se encuentra una coincidencia, el reproductor cambia primero al perfil de velocidad de bits coincidente en el manifiesto existente y cambia al perfil de tasa de bits coincidente en el manifiesto actualizado. Esto garantiza que la transición sea fluida.
   * Si no hay una tasa de bits común entre el manifiesto anterior y el nuevo, o si el TVSDK del explorador no puede cambiar a la velocidad de bits que coincida, el TVSDK del explorador cambia directamente al perfil de velocidad de bits más bajo del nuevo manifiesto y utiliza ABR para cambiar a cualquier tasa de bits permitida en función del ancho de banda. Esto puede provocar un ligero fallo en la reproducción, pero debe tener un impacto mínimo.

1. Si la actualización se realiza correctamente, el SDK de TVSDK del explorador envía un evento `MediaPlayerItemEvent.MASTER_UPDATED`.
1. Si la actualización no se realiza correctamente, la reproducción continúa con la configuración desde antes de esta actualización.

## Ejemplo 1 {#example_DB55F2B9D98741628C9B973E47A0B6A0}

Las siguientes tasas de bits están emitiendo en directo:

* 500k
* 900k
* 2100k

El flujo de 2100.000 tiene algunos problemas, por lo que debe reiniciarse. El manifiesto maestro se actualiza para contener solo 500 k y 900 k. Poco después, los usuarios que vean este programa a 2100k experimentarán un cambio en la velocidad de bits a 900k. Los usuarios que ven a las 900k siguen viendo a las 900k. Posteriormente, la secuencia de 2100.000 se reanuda y se vuelve a añadir en el manifiesto maestro. Poco después, los usuarios que ven a 900k, y tienen el ancho de banda, cambian a 2100k.

### Ejemplo 2 {#example_485E9A9F373D454CADE5395DEC734E5D}

Las siguientes tasas de bits están emitiendo en directo:

* 500k
* 900k
* 2100k

Es necesario reiniciar todas estas tasas de bits. Hay dos flujos temporales configurados para esto, a 400k y 1500k. Los usuarios cambian a 400k, que es la tasa de bits más baja de la nueva configuración. Algunos usuarios cambian a 1500 k cuando su ancho de banda es suficiente. Posteriormente, las tres tasas de bits vuelven a subir y se actualiza el manifiesto maestro. Los usuarios vuelven automáticamente a ver a 500k, que es el ancho de banda más bajo en el manifiesto revisado (original). Poco después, los usuarios se cambian al ancho de banda más alto (900k o 1200k) que su red permite.

<!-- 

WRITER: Add relref to api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#MASTER_UPDATED

 -->

