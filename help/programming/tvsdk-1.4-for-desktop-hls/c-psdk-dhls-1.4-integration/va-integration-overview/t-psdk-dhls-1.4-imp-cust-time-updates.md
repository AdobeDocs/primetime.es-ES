---
description: En determinadas implementaciones de análisis, es posible que la aplicación cliente desee proporcionar una posición de cursor de reproducción diferente a la indicada en el valor localTime de TVSDK. Por ejemplo, durante la reproducción de un flujo LINEAR, se puede proporcionar el cursor de reproducción de cada programa en relación con su tiempo de inicio.
seo-description: En determinadas implementaciones de análisis, es posible que la aplicación cliente desee proporcionar una posición de cursor de reproducción diferente a la indicada en el valor localTime de TVSDK. Por ejemplo, durante la reproducción de un flujo LINEAR, se puede proporcionar el cursor de reproducción de cada programa en relación con su tiempo de inicio.
seo-title: Implementar actualizaciones de tiempo personalizadas
title: Implementar actualizaciones de tiempo personalizadas
uuid: 2b46eca9-3815-4c44-ab5e-21678c35f410
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# Implementar actualizaciones de tiempo personalizadas{#implement-custom-time-updates}

En determinadas implementaciones de análisis, es posible que la aplicación cliente desee proporcionar una posición de cursor de reproducción diferente a la indicada en el valor localTime de TVSDK. Por ejemplo, durante la reproducción de un flujo LINEAR, se puede proporcionar el cursor de reproducción de cada programa en relación con su tiempo de inicio.

>[!TIP]
>
>Sobrescriba este método solo si desea proporcionar una posición de cabeza lectora diferente a la posición predeterminada.

1. Para anular la posición predeterminada del cursor de reproducción:

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
   >Los valores de este fragmento de código son solo ejemplos. Debe utilizar valores diferentes para la posición personalizada del cursor de reproducción.

