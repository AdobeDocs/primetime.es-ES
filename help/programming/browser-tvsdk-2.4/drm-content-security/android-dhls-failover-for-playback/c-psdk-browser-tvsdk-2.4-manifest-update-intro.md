---
description: El TVSDK del explorador puede detectar información de reproducción modificada en manifiestos m3u8 maestros para flujo en directo y actualizar la información de reproducción mientras se reproduce el flujo. TVSDK del explorador admite un conjunto dinámico de perfiles de velocidad de bits a medida que los perfiles aparecen o desaparecen del manifiesto principal, incluidas las tasas de bits de perfil no superpuestas entre actualizaciones.
title: Actualización activa del manifiesto maestro
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# Actualización activa del manifiesto maestro{#live-master-manifest-update}

El TVSDK del explorador puede detectar información de reproducción modificada en manifiestos m3u8 maestros para flujo en directo y actualizar la información de reproducción mientras se reproduce el flujo. TVSDK del explorador admite un conjunto dinámico de perfiles de velocidad de bits a medida que los perfiles aparecen o desaparecen del manifiesto principal, incluidas las tasas de bits de perfil no superpuestas entre actualizaciones.

Se admiten las siguientes funciones:

* Recuento de perfiles (aumento o disminución)
* Velocidades de bits de perfil (superpuestas o no superpuestas)
* Perfiles con direcciones URL en los mismos servidores (o en diferentes)
* Cualquier estructura de failover

Deben cumplirse todas las condiciones siguientes:

* La emisión está activa.
* Tanto la hora como la etiqueta cambian.
* Toda la información de representación sigue siendo la misma (excepto que las direcciones URL pueden variar).
* La información de acceso DRM permanece igual.
* Los segmentos se empaquetan en torno a los mismos límites de PTS y de fotogramas en un pequeño intervalo de errores.
