---
description: En algunas implementaciones de análisis, es posible que la aplicación cliente desee proporcionar una posición de cursor de reproducción diferente a la que indica el valor localTime del TVSDK del explorador.
seo-description: En algunas implementaciones de análisis, es posible que la aplicación cliente desee proporcionar una posición de cursor de reproducción diferente a la que indica el valor localTime del TVSDK del explorador.
seo-title: Implementar actualizaciones de tiempo personalizadas
title: Implementar actualizaciones de tiempo personalizadas
uuid: 26a0592c-a47b-4d65-b984-5e51533dcddc
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---


# Implementar actualizaciones de tiempo personalizadas{#implement-custom-time-updates}

En algunas implementaciones de análisis, es posible que la aplicación cliente desee proporcionar una posición de cursor de reproducción diferente a la que indica el valor localTime del TVSDK del explorador.

Por ejemplo, durante una reproducción de flujo lineal, se puede proporcionar el cursor de reproducción de cada programa en relación con su tiempo de inicio.

>[!TIP]
>
>Sobrescriba este método solo si desea proporcionar una posición de cabeza lectora distinta de la posición predeterminada.

Para anular la posición predeterminada del cursor de reproducción:

```js
vaMetadata.currentTimeUpdateBlock = function() { 
       return playerPositionInSeconds; 
}; 
```

>[!IMPORTANT]
>
>Los valores de este fragmento de código son solo ejemplos. Debe utilizar valores diferentes para la posición personalizada del cursor de reproducción.

