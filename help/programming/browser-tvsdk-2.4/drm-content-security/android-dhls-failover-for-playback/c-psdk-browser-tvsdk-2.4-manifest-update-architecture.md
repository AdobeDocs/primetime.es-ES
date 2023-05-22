---
description: A continuación se proporciona información y ejemplos sobre cómo el TVSDK del explorador admite manifiestos principales actualizados.
title: Arquitectura de actualización del manifiesto principal activa
exl-id: 2d9be228-7a96-4c19-828d-c1a4b0b07aa0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 1%

---

# Arquitectura de actualización del manifiesto principal activa{#live-master-manifest-update-architecture}

A continuación se proporciona información y ejemplos sobre cómo el TVSDK del explorador admite manifiestos principales actualizados.

Esta función está desactivada de forma predeterminada. Si la aplicación la activa estableciendo una frecuencia de actualización en minutos, se producirán los pasos siguientes después de cada intervalo de actualización:

1. El TVSDK del explorador comprueba la hora y la etiqueta de la última modificación del manifiesto maestro para determinar si el archivo se ha actualizado.

   Si han cambiado tanto la hora como la etiqueta, el archivo se considera modificado.
1. El TVSDK del explorador analiza el nuevo manifiesto y toma las medidas adecuadas en función de la naturaleza de la actualización.
1. Si la velocidad de bits de reproducción actual coincide con la velocidad de bits del manifiesto modificado, el TVSDK del explorador cambia al nuevo perfil.

   El nuevo perfil puede ser de un servidor diferente o del mismo servidor, con la misma velocidad de bits. En este caso, la transición es suave.
1. Si la velocidad de bits de reproducción actual ya no está presente en el nuevo manifiesto, el TVSDK del explorador intenta encontrar una velocidad de bits en el perfil actual que también exista en el nuevo manifiesto.

   * Si se encuentra una coincidencia, el reproductor primero cambia al perfil de velocidad de bits coincidente del manifiesto existente y cambia al perfil de velocidad de bits coincidente del manifiesto actualizado. Esto garantiza que la transición sea fluida.
   * Si no hay una velocidad de bits en común entre el manifiesto anterior y el nuevo, o si el TVSDK del explorador no puede cambiar a la velocidad de bits que coincida, el TVSDK del explorador cambia directamente al perfil de velocidad de bits más baja del nuevo manifiesto y utiliza ABR para cambiar a cualquier velocidad de bits permitida en función del ancho de banda. Esto puede provocar un ligero fallo en la reproducción, pero debería tener un impacto mínimo.

1. Si la actualización se realiza correctamente, el TVSDK del explorador envía un `MediaPlayerItemEvent.MASTER_UPDATED` evento.
1. Si la actualización no se realiza correctamente, la reproducción continúa con la configuración de antes de esta actualización.

## Ejemplo 1 {#example_DB55F2B9D98741628C9B973E47A0B6A0}

Las siguientes tasas de bits se transmiten en vivo:

* 500k
* 900k
* 2100k

El flujo de 2100k tiene algunos problemas, por lo que debe reiniciarse. El manifiesto principal se actualiza para contener solo 500 K y 900 K. Poco después, los usuarios que vean este programa a 2100k experimentarán un cambio de velocidad de bits a 900k. Los usuarios que ven a 900.000 siguen viendo a 900.000. Posteriormente, la secuencia de 2100 K se reanuda y se agrega de nuevo en el manifiesto principal. Un tiempo después, los usuarios que ven a 900k, y tienen el ancho de banda, cambian a 2100k.

### Ejemplo 2 {#example_485E9A9F373D454CADE5395DEC734E5D}

Las siguientes tasas de bits se transmiten en vivo:

* 500k
* 900k
* 2100k

Es necesario reiniciar todas estas velocidades de bits. Hay dos flujos temporales configurados para esto, a 400k y 1500k. Los usuarios se cambian a 400.000, que es la velocidad de bits más baja de la nueva configuración. Algunos de los usuarios se cambian a 1500.000 cuando su ancho de banda es suficiente. Más adelante, se realiza una copia de seguridad de las tres velocidades de bits y se actualiza el manifiesto maestro. Los usuarios vuelven automáticamente a ver a 500.000, que es el ancho de banda más bajo en el manifiesto revisado (original). Un tiempo después, los usuarios pasan al ancho de banda más alto (900k o 1200k) que permite su red.

<!-- 

WRITER: Add relref to api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#MASTER_UPDATED

 -->
