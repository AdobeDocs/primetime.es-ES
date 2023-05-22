---
description: Puede elegir utilizar comportamientos de anuncio predeterminados.
title: Usar el comportamiento de reproducción predeterminado
exl-id: c277db2a-546e-4097-96ce-83914b726576
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '60'
ht-degree: 0%

---

# Usar el comportamiento de reproducción predeterminado {#use-the-default-playback-behavior}

Puede elegir utilizar comportamientos de anuncio predeterminados.

Para utilizar comportamientos predeterminados:

    * Si implementa su propia clase AdvertisingFactory, devuelva un valor nulo para createAdPolicySelector.
    
    * Si no tiene una implementación personalizada para la clase AdvertisingFactory, TVSDK utiliza un selector de políticas de publicidad predeterminado
