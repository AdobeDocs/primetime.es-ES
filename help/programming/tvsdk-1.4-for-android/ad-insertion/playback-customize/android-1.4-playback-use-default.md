---
description: Puede elegir utilizar comportamientos de anuncio predeterminados.
title: Usar el comportamiento de reproducción predeterminado
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---

# Usar el comportamiento de reproducción predeterminado {#use-the-default-playback-behavior}

Puede elegir utilizar comportamientos de anuncio predeterminados.

Para utilizar comportamientos predeterminados:

    * Si implementa su propia clase AdvertisingFactory, devuelva un valor nulo para createAdPolicySelector.
    
    * Si no tiene una implementación personalizada para la clase AdvertisingFactory, TVSDK utiliza un selector de políticas de publicidad predeterminado
