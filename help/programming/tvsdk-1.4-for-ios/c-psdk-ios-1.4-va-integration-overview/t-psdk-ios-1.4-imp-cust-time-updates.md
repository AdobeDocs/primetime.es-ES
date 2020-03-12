---
description: En algunas implementaciones de análisis, es posible que la aplicación cliente desee proporcionar una posición de cursor de reproducción diferente a la que indica el valor localTime del TVSDK. Por ejemplo, durante una reproducción de flujo lineal, se puede proporcionar el cursor de reproducción de cada programa en relación con su tiempo de inicio.
seo-description: En algunas implementaciones de análisis, es posible que la aplicación cliente desee proporcionar una posición de cursor de reproducción diferente a la que indica el valor localTime del TVSDK. Por ejemplo, durante una reproducción de flujo lineal, se puede proporcionar el cursor de reproducción de cada programa en relación con su tiempo de inicio.
seo-title: Implementar actualizaciones de tiempo personalizadas
title: Implementar actualizaciones de tiempo personalizadas
uuid: 303303eb-c371-4766-a1ee-806ba75b4e01
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Implementar actualizaciones de tiempo personalizadas{#implement-custom-time-updates}

En algunas implementaciones de análisis, es posible que la aplicación cliente desee proporcionar una posición de cursor de reproducción diferente a la que indica el valor localTime del TVSDK. Por ejemplo, durante una reproducción de flujo lineal, se puede proporcionar el cursor de reproducción de cada programa en relación con su tiempo de inicio.

>[!TIP]
>
>Sobrescriba este método solo si desea proporcionar una posición de cabeza lectora distinta de la posición predeterminada.

1. Para anular la posición predeterminada del cursor de reproducción:

   ```
   vaTrackingMetadata.currentTimeUpdateBlock = ^CMTime () { 
       NSInteger random = arc4random() % 500;  
       return CMTimeMakeWithSeconds(random, 1); 
   };
   ```

   >[!IMPORTANT]
   >
   >En este ejemplo de código, 500 es sólo un valor de muestra. Debe utilizar un valor diferente para la posición personalizada del cursor de reproducción.

