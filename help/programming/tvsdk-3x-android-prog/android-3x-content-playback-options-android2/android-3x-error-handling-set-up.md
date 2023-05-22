---
description: Puede configurar un lugar para gestionar errores.
title: Configuración de la gestión de errores
exl-id: 9b83b47e-6d30-452b-87c3-1e3a139f2e69
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# Configuración de la gestión de errores {#set-up-error-handling}

Puede configurar un lugar para gestionar errores.

1. Implementación de una función de llamada de retorno para `MediaPlayerEvent.STATUS_CHANGED`.

   TVSDK pasa información de evento, como un `MediaPlayerStatusChangeEvent` objeto.
1. En la llamada de retorno, cuando el estado devuelto es `MediaPlayerStatus.ERROR`, proporcione lógica para gestionar todos los errores.
1. Una vez gestionado el error, restablezca el `MediaPlayer` o cargar un nuevo recurso de medios.

   Si la variable `MediaPlayer` el objeto está en estado de error y permanecerá en ese estado hasta que lo restablezca con el `MediaPlayer.reset` método.

<!--<a id="example_E74BB605ED08450295B8902F1E4BB8F5"></a>-->

Por ejemplo:

```java
mediaPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED,  
  new StatusChangeEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
        if (event.getStatus() == MediaPlayerStatus.ERROR) { 
        // handle TVSDK error here 
        } 
    } 
});
```
