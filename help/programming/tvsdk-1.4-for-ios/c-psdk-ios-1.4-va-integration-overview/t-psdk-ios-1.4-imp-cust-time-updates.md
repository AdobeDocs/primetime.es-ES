---
description: En algunas implementaciones de analytics, es posible que la aplicación cliente desee proporcionar una posición de cabezal de reproducción diferente a la que indica el valor localTime del TVSDK. Por ejemplo, durante una reproducción de flujo lineal, se puede proporcionar el cabezal de reproducción de cada programa en relación con su tiempo de inicio.
title: Implementar actualizaciones de tiempo personalizadas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---


# Implementar actualizaciones de tiempo personalizadas{#implement-custom-time-updates}

En algunas implementaciones de analytics, es posible que la aplicación cliente desee proporcionar una posición de cabezal de reproducción diferente a la que indica el valor localTime del TVSDK. Por ejemplo, durante una reproducción de flujo lineal, se puede proporcionar el cabezal de reproducción de cada programa en relación con su tiempo de inicio.

>[!TIP]
>
>Sobrescriba este método solo si desea proporcionar una posición del cabezal de reproducción diferente de la posición predeterminada.

1. Para anular la posición predeterminada del cabezal de reproducción:

   ```
   vaTrackingMetadata.currentTimeUpdateBlock = ^CMTime () { 
       NSInteger random = arc4random() % 500;  
       return CMTimeMakeWithSeconds(random, 1); 
   };
   ```

   >[!IMPORTANT]
   >
   >En este ejemplo de código, 500 es solo un valor de muestra. Debe utilizar un valor diferente para la posición del cabezal de reproducción personalizado.

