---
description: En algunas implementaciones de análisis, es posible que la aplicación cliente desee proporcionar una posición de cursor de reproducción diferente a la que indica el valor localTime de TVSDK. Por ejemplo, durante una reproducción de flujo lineal, se puede proporcionar el cursor de reproducción de cada programa en relación con su tiempo de inicio.
seo-description: En algunas implementaciones de análisis, es posible que la aplicación cliente desee proporcionar una posición de cursor de reproducción diferente a la que indica el valor localTime de TVSDK. Por ejemplo, durante una reproducción de flujo lineal, se puede proporcionar el cursor de reproducción de cada programa en relación con su tiempo de inicio.
seo-title: Implementar actualizaciones de tiempo personalizadas
title: Implementar actualizaciones de tiempo personalizadas
uuid: 7f5d46e5-eab6-4bdc-b015-ae27ddb609ce
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# Implementar actualizaciones de tiempo personalizadas {#implement-custom-time-updates}

En algunas implementaciones de análisis, es posible que la aplicación cliente desee proporcionar una posición de cursor de reproducción diferente a la que indica el valor localTime de TVSDK. Por ejemplo, durante una reproducción de flujo lineal, se puede proporcionar el cursor de reproducción de cada programa en relación con su tiempo de inicio.

>[!TIP]
>
>Sobrescriba este método solo si desea proporcionar una posición de cabeza lectora distinta de la posición predeterminada.

Para anular la posición predeterminada del cursor de reproducción:

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
>Los valores de este fragmento de código son solo ejemplos. Debe utilizar valores diferentes para la posición personalizada del cursor de reproducción.