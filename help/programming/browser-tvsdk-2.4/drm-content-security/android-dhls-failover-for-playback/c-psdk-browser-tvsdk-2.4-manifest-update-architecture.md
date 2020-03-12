---
description: A continuación se proporcionan algunos ejemplos e información sobre cómo el TVSDK del explorador adapta los manifiestos maestros actualizados.
seo-description: A continuación se proporcionan algunos ejemplos e información sobre cómo el TVSDK del explorador adapta los manifiestos maestros actualizados.
seo-title: Arquitectura de actualización de manifiesto maestro activa
title: Arquitectura de actualización de manifiesto maestro activa
uuid: 6f253502-8dec-4b42-9ee1-99ad9bfd6080
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Arquitectura de actualización de manifiesto maestro activa{#live-master-manifest-update-architecture}

A continuación se proporcionan algunos ejemplos e información sobre cómo el TVSDK del explorador adapta los manifiestos maestros actualizados.

De forma predeterminada, esta función está desactivada. Si la aplicación la activa configurando una frecuencia de actualización en minutos, después de cada intervalo de actualización se dan los siguientes pasos:

1. El TVSDK del explorador comprueba la hora y la etiqueta de la última modificación del manifiesto maestro para determinar si el archivo se ha actualizado.

   Si la hora y la etiqueta han cambiado, el archivo se considera modificado.
1. El TVSDK del explorador analiza y analiza el nuevo manifiesto y toma las medidas adecuadas en función de la naturaleza de la actualización.
1. Si la velocidad de bits de reproducción actual coincide con la velocidad de bits del manifiesto modificado, el TVSDK del explorador cambia al nuevo perfil.

   El nuevo perfil puede ser de un servidor diferente o del mismo servidor, a la misma velocidad de bits. En este caso, la transición es fluida.
1. Si la velocidad de bits de reproducción actual ya no está presente en el nuevo manifiesto, el TVSDK del explorador intenta encontrar una velocidad de bits en el perfil actual que también existe en el nuevo manifiesto.

   * Si se encuentra una coincidencia, el reproductor primero cambia al perfil de velocidad de bits coincidente en el manifiesto existente y pasa al perfil de velocidad de bits coincidente en el manifiesto actualizado. Esto garantiza que la transición sea fluida.
   * Si no hay una velocidad de bits común entre el manifiesto anterior y el nuevo, o si el TVSDK del explorador no puede cambiar a la velocidad de bits que coincide, el TVSDK del explorador cambia directamente al perfil de velocidad de bits más bajo del nuevo manifiesto y utiliza ABR para cambiar a cualquier velocidad de bits permitida en función del ancho de banda. Esto puede provocar un ligero fallo en la reproducción, pero debe tener un impacto mínimo.

1. Si la actualización se realiza correctamente, el SDK de TVSDK del explorador distribuye un `MediaPlayerItemEvent.MASTER_UPDATED` evento.
1. Si la actualización no se realiza correctamente, la reproducción continúa con la configuración desde antes de esta actualización.

## Ejemplo 1 {#example_DB55F2B9D98741628C9B973E47A0B6A0}

Las siguientes velocidades de bits se están retransmitiendo en directo:

* 500k
* 900k
* 2100k

El flujo de 2100k tiene algunos problemas, por lo que debe reiniciarse. El manifiesto maestro se actualiza para contener solo 500k y 900k. Poco después, los usuarios que ven este programa a 2100k experimentarán un cambio de velocidad de bits a 900k. Los usuarios que miran a 900k siguen viendo a 900k. Más adelante, se reanuda el flujo de 2100.000 y se vuelve a agregar al manifiesto maestro. Poco después, los usuarios que miran a 900k, y tienen el ancho de banda, se cambian a 2100k.

### Ejemplo 2 {#example_485E9A9F373D454CADE5395DEC734E5D}

Las siguientes velocidades de bits se están retransmitiendo en directo:

* 500k
* 900k
* 2100k

Es necesario reiniciar todas estas velocidades de bits. Hay dos corrientes temporales configuradas para esto, a 400k y 1500k. Los usuarios se cambian a 400k, que es la velocidad de bits más baja de la nueva configuración. Algunos usuarios pasan a 1500.000 cuando su ancho de banda es suficiente. Más adelante, las tres velocidades de bits vuelven a aparecer y se actualiza el manifiesto maestro. Los usuarios regresan automáticamente para mirar a 500 k, que es el ancho de banda más bajo en el manifiesto (original) revisado. Un tiempo después, los usuarios se cambian al ancho de banda más alto (900k o 1200k) que su red permite.

<!-- 

WRITER: Add relref to api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#MASTER_UPDATED

 -->

