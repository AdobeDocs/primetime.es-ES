---
description: En algunas implementaciones de Analytics, es posible que la aplicación cliente desee proporcionar una posición de cabezal de reproducción diferente a la posición indicada por el valor localTime de TVSDK. Por ejemplo, durante una reproducción de flujo lineal, se puede proporcionar el cabezal de reproducción de cada programa en relación con su hora de inicio.
title: Implementación de actualizaciones de tiempo personalizadas
exl-id: 91e778ca-cdab-4c50-96f8-3333d210fd4a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Implementación de actualizaciones de tiempo personalizadas {#implement-custom-time-updates}

En algunas implementaciones de Analytics, es posible que la aplicación cliente desee proporcionar una posición de cabezal de reproducción diferente a la posición indicada por el valor localTime de TVSDK. Por ejemplo, durante una reproducción de flujo lineal, se puede proporcionar el cabezal de reproducción de cada programa en relación con su hora de inicio.

>[!TIP]
>
>Anule este método solo si desea proporcionar una posición del cabezal de reproducción distinta a la posición predeterminada.

Para anular la posición predeterminada del cabezal de reproducción:

```java
vaMetadata.setCurrentTimeUpdateBlock(new VideoAnalyticsMetadata.CurrentTimeUpdateBlock() { 
    @Override 
    public long call() { 
        long range = 500L; 
        Random r = new Random() 
        return (long)(r.nextDouble()*range); 
    } 
});
```

>[!IMPORTANT]
>
>Los valores de este fragmento de código son solo ejemplos. Debe utilizar valores diferentes para la posición personalizada del cabezal de reproducción.
