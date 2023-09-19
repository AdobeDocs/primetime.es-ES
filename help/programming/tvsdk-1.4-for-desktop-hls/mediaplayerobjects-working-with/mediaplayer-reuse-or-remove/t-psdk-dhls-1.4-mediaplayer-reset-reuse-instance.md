---
description: Cuando restablece una instancia de MediaPlayer, vuelve a su estado IDLE sin inicializar tal como se define en MediaPlayerStatus.
title: Restablecer o reutilizar una instancia de MediaPlayer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# Restablecer o reutilizar una instancia de MediaPlayer{#reset-or-reuse-a-mediaplayer-instance}

Puede restablecer, reutilizar o liberar una instancia de MediaPlayer que ya no necesite.

Cuando restablece una instancia de MediaPlayer, vuelve a su estado IDLE sin inicializar tal como se define en MediaPlayerStatus.

Esta operación resulta útil en los siguientes casos:

* Desea volver a utilizar un `MediaPlayer` instancia, pero debe cargar una nueva `MediaResource` (contenido de vídeo) y reemplace la instancia anterior.

  El restablecimiento le permite reutilizar el `MediaPlayer` instancia sin los gastos generales de liberación de recursos, recreando la `MediaPlayer`y la reasignación de recursos. El `replaceCurrentItem` y `replaceCurrentResource` Los métodos de realizan automáticamente estos pasos, sin tener que llamar al método reset.

* Si la variable `MediaPlayer` tiene un estado ERROR y debe borrarse.

  >[!IMPORTANT]
  >
  >Esta es la única manera de recuperarse del estado de ERROR.

1. Llamada `reset` para devolver el `MediaPlayer` a su estado sin inicializar:

   ```
   function reset():void; 
   ```

1. Uso `MediaPlayer.replaceCurrentItem` o `MediaPlayer.replaceCurrentResource` para cargar otro `MediaResource`.

   >[!TIP]
   >
   >Para borrar un error, cargue el mismo `MediaResource`.

1. Cuando reciba la `MediaPlaybackStatusChangeEvent.STATUS_CHANGED` con el `PREPARED` estado, inicie la reproducción.
