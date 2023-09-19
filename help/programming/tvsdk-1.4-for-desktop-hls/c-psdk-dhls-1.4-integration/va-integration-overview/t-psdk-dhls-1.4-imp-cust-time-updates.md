---
description: En determinadas implementaciones de análisis, es posible que la aplicación cliente desee proporcionar una posición de cabezal de reproducción diferente a la indicada por el valor localTime de TVSDK. Por ejemplo, durante una reproducción de flujo LINEAL, se puede proporcionar el cabezal de reproducción de cada programa en relación con su hora de inicio.
title: Implementación de actualizaciones de tiempo personalizadas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Implementación de actualizaciones de tiempo personalizadas{#implement-custom-time-updates}

En determinadas implementaciones de análisis, es posible que la aplicación cliente desee proporcionar una posición de cabezal de reproducción diferente a la indicada por el valor localTime de TVSDK. Por ejemplo, durante una reproducción de flujo LINEAL, se puede proporcionar el cabezal de reproducción de cada programa en relación con su hora de inicio.

>[!TIP]
>
>Anule este método solo si desea proporcionar una posición de cabezal de reproducción diferente a la posición predeterminada.

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
   >Los valores de este fragmento de código son solo ejemplos. Debe utilizar valores diferentes para la posición personalizada del cabezal de reproducción.
