---
description: El SDK del explorador puede detectar información de reproducción modificada en los manifiestos m3u8 maestros para flujo continuo en directo y actualizar la información de reproducción mientras se reproduce el flujo. El SDK TVSDK del explorador admite un conjunto dinámico de perfiles de velocidad de bits a medida que los perfiles aparecen o desaparecen del manifiesto maestro, incluidas las velocidades de bits de perfil no superpuestas entre actualizaciones.
seo-description: El SDK del explorador puede detectar información de reproducción modificada en los manifiestos m3u8 maestros para flujo continuo en directo y actualizar la información de reproducción mientras se reproduce el flujo. El SDK TVSDK del explorador admite un conjunto dinámico de perfiles de velocidad de bits a medida que los perfiles aparecen o desaparecen del manifiesto maestro, incluidas las velocidades de bits de perfil no superpuestas entre actualizaciones.
seo-title: Actualización de manifiesto maestro activo
title: Actualización de manifiesto maestro activo
uuid: 4b918a73-dacf-465a-82d6-404c6bdb01f2
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Actualización de manifiesto maestro activo{#live-master-manifest-update}

El SDK del explorador puede detectar información de reproducción modificada en los manifiestos m3u8 maestros para flujo continuo en directo y actualizar la información de reproducción mientras se reproduce el flujo. El SDK TVSDK del explorador admite un conjunto dinámico de perfiles de velocidad de bits a medida que los perfiles aparecen o desaparecen del manifiesto maestro, incluidas las velocidades de bits de perfil no superpuestas entre actualizaciones.

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

