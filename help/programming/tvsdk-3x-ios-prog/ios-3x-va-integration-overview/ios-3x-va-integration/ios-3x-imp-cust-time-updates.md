---
description: En algunas implementaciones de análisis, es posible que la aplicación cliente desee proporcionar una posición de cursor de reproducción diferente a la que indica el valor localTime del TVSDK. Por ejemplo, durante una reproducción de flujo lineal, se puede proporcionar el cursor de reproducción de cada programa en relación con su tiempo de inicio.
seo-description: En algunas implementaciones de análisis, es posible que la aplicación cliente desee proporcionar una posición de cursor de reproducción diferente a la que indica el valor localTime del TVSDK. Por ejemplo, durante una reproducción de flujo lineal, se puede proporcionar el cursor de reproducción de cada programa en relación con su tiempo de inicio.
seo-title: Implementar actualizaciones de tiempo personalizadas
title: Implementar actualizaciones de tiempo personalizadas
uuid: 174937ca-3c26-4385-a298-8a01fc93ea20
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# Implementar actualizaciones de tiempo personalizadas {#implement-custom-time-updates}

En algunas implementaciones de análisis, es posible que la aplicación cliente desee proporcionar una posición de cursor de reproducción diferente a la que indica el valor localTime del TVSDK. Por ejemplo, durante una reproducción de flujo lineal, se puede proporcionar el cursor de reproducción de cada programa en relación con su tiempo de inicio.

>[!TIP]
>
>Sobrescriba este método solo si desea proporcionar una posición de cabeza lectora distinta de la posición predeterminada.

Para anular la posición predeterminada del cursor de reproducción:

```
vaTrackingMetadata.currentTimeUpdateBlock = ^CMTime () { 
    NSInteger random = arc4random() % 500;  
    return CMTimeMakeWithSeconds(random, 1); 
};
```

>[!IMPORTANT]
>
>En este ejemplo de código, 500 es sólo un valor de muestra. Debe utilizar un valor diferente para la posición personalizada del cursor de reproducción.