---
description: En algunas implementaciones de analytics, es posible que la aplicación cliente desee proporcionar una posición de cabezal de reproducción diferente a la registrada en el valor localTime de TVSDK. Por ejemplo, durante la reproducción de un flujo LINEAR, se puede proporcionar el cabezal de reproducción de cada programa en relación con su tiempo de inicio.
title: Implementar actualizaciones de tiempo personalizadas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# Implementar actualizaciones de tiempo personalizadas{#implement-custom-time-updates}

En algunas implementaciones de analytics, es posible que la aplicación cliente desee proporcionar una posición de cabezal de reproducción diferente a la registrada en el valor localTime de TVSDK. Por ejemplo, durante la reproducción de un flujo LINEAR, se puede proporcionar el cabezal de reproducción de cada programa en relación con su tiempo de inicio.

>[!TIP]
>
>Sobrescriba este método solo si desea proporcionar una posición de cabezal de reproducción diferente a la predeterminada.

1. Para anular la posición predeterminada del cabezal de reproducción:

   ```
   vaMetadata.currentTimeUpdateBlock = function():Number { 
      if (currentTime == 0) { 
          currentTime = getTimer(); 
      } 
      return ((getTimer() - currentTime) / 1000 + 1000); 
   }
   ```

   >[!IMPORTANT]
   >
   >Los valores de este fragmento de código son solo muestras. Debe utilizar valores diferentes para la posición del cabezal de reproducción personalizado.

