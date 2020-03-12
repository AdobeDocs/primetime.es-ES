---
description: TVSDK puede detectar información de reproducción modificada en los manifiestos m3u8 maestros para flujo continuo en directo y actualizar la información de reproducción mientras se reproduce el flujo. TVSDK admite un conjunto dinámico de perfiles de velocidad de bits a medida que los perfiles aparecen o desaparecen del manifiesto maestro, incluidas las velocidades de bits de perfil no superpuestas entre actualizaciones.
seo-description: TVSDK puede detectar información de reproducción modificada en los manifiestos m3u8 maestros para flujo continuo en directo y actualizar la información de reproducción mientras se reproduce el flujo. TVSDK admite un conjunto dinámico de perfiles de velocidad de bits a medida que los perfiles aparecen o desaparecen del manifiesto maestro, incluidas las velocidades de bits de perfil no superpuestas entre actualizaciones.
seo-title: Actualización de manifiesto maestro activo
title: Actualización de manifiesto maestro activo
uuid: 44f8adc2-0538-4c5d-8e39-55f661d8540b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Actualización de manifiesto maestro activo{#live-master-manifest-update}

TVSDK puede detectar información de reproducción modificada en los manifiestos m3u8 maestros para flujo continuo en directo y actualizar la información de reproducción mientras se reproduce el flujo. TVSDK admite un conjunto dinámico de perfiles de velocidad de bits a medida que los perfiles aparecen o desaparecen del manifiesto maestro, incluidas las velocidades de bits de perfil no superpuestas entre actualizaciones.

Se admiten las siguientes funciones:

* Recuento de perfiles (aumento o disminución)
* Frecuencias de bits de perfil (superposición o no superposición)
* Perfiles con direcciones URL en los mismos servidores (o en diferentes)
* Cualquier estructura de conmutación por error

Deben cumplirse todas las condiciones siguientes:

* El flujo está activo.
* Tanto el tiempo como la etiqueta cambian.
* Toda la información de representación sigue siendo la misma (excepto que las direcciones URL pueden variar).
* La información de acceso DRM sigue siendo la misma.
* Los segmentos se empaquetan alrededor de los mismos límites de fotogramas y PTS en un pequeño intervalo de errores.

## Arquitectura de actualización de manifiesto maestro activa {#section_32254A0F684B4960ACC33BF6B1AEF6F1}

A continuación encontrará información y ejemplos sobre cómo el TVSDK acomoda los manifiestos maestros actualizados.

De forma predeterminada, esta función está desactivada. Si la aplicación la activa configurando una frecuencia de actualización en minutos, después de cada intervalo de actualización se dan los siguientes pasos:

1. El TVSDK comprueba la hora y la etiqueta de la última modificación del manifiesto maestro para determinar si el archivo se ha actualizado.

   Si la hora y la etiqueta han cambiado, el archivo se considera modificado.
1. El TVSDK analiza y analiza el nuevo manifiesto y adopta las medidas adecuadas en función de la naturaleza de la actualización.
1. Si la velocidad de bits de reproducción actual coincide con la velocidad de bits del manifiesto modificado, el TVSDK cambia al nuevo perfil.

   El nuevo perfil puede ser de un servidor diferente o del mismo servidor, a la misma velocidad de bits. En este caso, la transición es fluida.
1. Si la velocidad de bits de reproducción actual ya no está presente en el nuevo manifiesto, el TVSDK intenta encontrar una velocidad de bits en el perfil actual que también existe en el nuevo manifiesto.

   * Si se encuentra una coincidencia, el reproductor primero cambia al perfil de velocidad de bits coincidente en el manifiesto existente y pasa al perfil de velocidad de bits coincidente en el manifiesto actualizado. Esto garantiza que la transición sea fluida.
   * Si no hay una velocidad de bits común entre el manifiesto anterior y el nuevo, o si el TVSDK no puede cambiar a la velocidad de bits que coincide, el TVSDK cambia directamente al perfil de velocidad de bits más bajo del nuevo manifiesto y utiliza ABR para cambiar a cualquier velocidad de bits permitida en función del ancho de banda. Esto puede provocar un ligero fallo en la reproducción, pero debe tener un impacto mínimo.

1. Si la actualización se realiza correctamente, el TVSDK distribuye un `MediaPlayerItemEvent.MASTER_UPDATED` evento.
1. Si la actualización no se realiza correctamente, la reproducción continúa con la configuración desde antes de esta actualización.

### Ejemplo 1 {#example_DB55F2B9D98741628C9B973E47A0B6A0}

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

## Usar actualización de maestro-manifiesto en directo {#section_34AC4A9751DB4B7C8561302C6A59A1C4}

Puede activar esta función y comprobar si hay eventos relacionados.

1. Para activar las actualizaciones de manifiesto maestro en vivo, establezca la frecuencia de actualización (en minutos) estableciendo la `NetworkConfiguration.masterUpdateInterval` propiedad.
1. De forma opcional, rastree las actualizaciones de manifiesto correctas escuchando el `MediaPlayerItemEvent.MASTER_UPDATED` evento.

