---
description: El TVSDK del explorador puede detectar información de reproducción modificada en manifiestos m3u8 maestros para flujo en directo y actualizar la información de reproducción mientras se reproduce el flujo. TVSDK del explorador admite un conjunto dinámico de perfiles de velocidad de bits a medida que los perfiles aparecen o desaparecen del manifiesto principal, incluidas las tasas de bits de perfil no superpuestas entre actualizaciones.
title: Actualización activa del manifiesto maestro
exl-id: 2f89131c-5204-465b-8757-b47e955f5894
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
