---
description: En algunas implementaciones de Analytics, es posible que la aplicación cliente desee proporcionar una posición de cabezal de reproducción diferente a la indicada por el valor de tiempo local de TVSDK del explorador.
title: Implementación de actualizaciones de tiempo personalizadas
exl-id: 4d045c4d-298a-42ae-af61-0463a76bc872
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Implementación de actualizaciones de tiempo personalizadas{#implement-custom-time-updates}

En algunas implementaciones de Analytics, es posible que la aplicación cliente desee proporcionar una posición de cabezal de reproducción diferente a la indicada por el valor de tiempo local de TVSDK del explorador.

Por ejemplo, durante una reproducción de flujo lineal, se puede proporcionar el cabezal de reproducción de cada programa en relación con su hora de inicio.

>[!TIP]
>
>Anule este método solo si desea proporcionar una posición del cabezal de reproducción distinta a la posición predeterminada.

Para anular la posición predeterminada del cabezal de reproducción:

```js
vaMetadata.currentTimeUpdateBlock = function() { 
       return playerPositionInSeconds; 
}; 
```

>[!IMPORTANT]
>
>Los valores de este fragmento de código son solo ejemplos. Debe utilizar valores diferentes para la posición personalizada del cabezal de reproducción.
