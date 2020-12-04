---
description: Puede elegir usar comportamientos de publicidad predeterminados.
seo-description: Puede elegir usar comportamientos de publicidad predeterminados.
seo-title: Usar el comportamiento de reproducción predeterminado
title: Usar el comportamiento de reproducción predeterminado
uuid: ccda5223-17c1-4cda-b875-e706f5dc8648
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Usar el comportamiento de reproducción predeterminado {#use-the-default-playback-behavior}

Puede elegir usar comportamientos de publicidad predeterminados.

Para utilizar comportamientos predeterminados:

    * Si implementa su propia clase &quot;AdvertisingFactory&quot;, devuelva null para &quot;createAdPolicySelector&quot;.
    
    * Si no tiene una implementación personalizada para la clase `AdvertisingFactory′, TVSDK utiliza un selector de directivas de publicidad predeterminado.