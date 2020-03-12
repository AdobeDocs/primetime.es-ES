---
description: Puede configurar un lugar para gestionar los errores.
seo-description: Puede configurar un lugar para gestionar los errores.
seo-title: Configurar la gestión de errores
title: Configurar la gestión de errores
uuid: fde47fa5-5ca5-4be5-a7e7-3227c5e4c670
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef

---


# Configurar la gestión de errores {#set-up-error-handling}

Puede configurar un lugar para gestionar los errores.

1. Implementar una función de llamada de retorno de evento para `MediaPlayerEvent.STATUS_CHANGED`.

   TVSDK pasa información de eventos, como un `MediaPlayerStatusChangeEvent` objeto.
1. En la llamada de retorno, cuando el estado devuelto sea `MediaPlayerStatus.ERROR`, proporcione lógica para gestionar todos los errores.
1. Después de gestionar el error, restablezca el `MediaPlayer` objeto o cargue un nuevo recurso de medios.

   Cuando el `MediaPlayer` objeto está en estado de error, permanece en ese estado hasta que se restablece con el `MediaPlayer.reset` método .

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

