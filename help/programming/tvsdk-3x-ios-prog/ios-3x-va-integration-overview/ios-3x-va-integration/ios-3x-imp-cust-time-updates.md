---
description: En algunas implementaciones de Analytics, es posible que la aplicación cliente desee proporcionar una posición de cabezal de reproducción diferente a la posición indicada por el valor localTime de TVSDK. Por ejemplo, durante una reproducción de flujo lineal, se puede proporcionar el cabezal de reproducción de cada programa en relación con su hora de inicio.
title: Implementación de actualizaciones de tiempo personalizadas
exl-id: df35d422-d9dc-496d-8f6f-cf34d82ab046
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# Implementación de actualizaciones de tiempo personalizadas {#implement-custom-time-updates}

En algunas implementaciones de Analytics, es posible que la aplicación cliente desee proporcionar una posición de cabezal de reproducción diferente a la posición indicada por el valor localTime de TVSDK. Por ejemplo, durante una reproducción de flujo lineal, se puede proporcionar el cabezal de reproducción de cada programa en relación con su hora de inicio.

>[!TIP]
>
>Anule este método solo si desea proporcionar una posición del cabezal de reproducción diferente de la posición predeterminada.

Para anular la posición predeterminada del cabezal de reproducción:

```
vaTrackingMetadata.currentTimeUpdateBlock = ^CMTime () { 
    NSInteger random = arc4random() % 500;  
    return CMTimeMakeWithSeconds(random, 1); 
};
```

>[!IMPORTANT]
>
>En este ejemplo de código, 500 es solo un valor de muestra. Debe utilizar un valor diferente para la posición personalizada del cabezal de reproducción.
