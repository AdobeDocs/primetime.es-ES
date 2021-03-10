---
description: El SDK del explorador puede detectar la información de reproducción modificada en los manifiestos maestros m3u8 para la transmisión en directo y actualizar la información de reproducción mientras se reproduce la emisión. El SDK de explorador admite un conjunto dinámico de perfiles de velocidad de bits a medida que los perfiles aparecen o desaparecen del manifiesto maestro, incluidas las tasas de bits de perfil no superpuestas entre actualizaciones.
title: Actualización del manifiesto maestro activo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# Actualización del manifiesto maestro activo{#live-master-manifest-update}

El SDK del explorador puede detectar la información de reproducción modificada en los manifiestos maestros m3u8 para la transmisión en directo y actualizar la información de reproducción mientras se reproduce la emisión. El SDK de explorador admite un conjunto dinámico de perfiles de velocidad de bits a medida que los perfiles aparecen o desaparecen del manifiesto maestro, incluidas las tasas de bits de perfil no superpuestas entre actualizaciones.

Se admiten las siguientes funciones:

* Recuento de perfiles (aumento o disminución)
* Tasas de bits de perfil (superpuestas o no superpuestas)
* Perfiles con direcciones URL en los mismos servidores (o diferentes)
* Cualquier estructura de failover

Deben cumplirse todas las condiciones siguientes:

* La emisión está activa.
* Tanto el tiempo como la etiqueta cambian.
* Toda la información de representación sigue siendo la misma (excepto que las direcciones URL pueden variar).
* La información de acceso de DRM sigue siendo la misma.
* Los segmentos se empaquetan alrededor de los mismos límites de PTS y fotogramas en un pequeño intervalo de errores.

