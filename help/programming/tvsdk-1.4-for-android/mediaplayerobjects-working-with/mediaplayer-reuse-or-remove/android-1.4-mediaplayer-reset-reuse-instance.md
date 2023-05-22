---
description: Cuando restablece una instancia de MediaPlayer, vuelve a su estado IDLE sin inicializar tal como se define en MediaPlayerState.
title: Restablecer o reutilizar una instancia de MediaPlayer
exl-id: db8264f7-2f33-4441-86db-bb985edf7c3c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---

# Restablecer, reutilizar o quitar una instancia de MediaPlayer {#reset-or-reuse-a-mediaplayer-instance}

Puede restablecer, reutilizar o liberar una instancia de MediaPlayer que ya no necesite.

Cuando restablece una instancia de MediaPlayer, vuelve a su estado IDLE sin inicializar tal como se define en MediaPlayerState.

Esta operación resulta útil en los siguientes casos:

* Desea volver a utilizar un `MediaPlayer` instancia, pero debe cargar una nueva `MediaResource` (contenido de vídeo) y reemplace la instancia anterior.

   El restablecimiento le permite reutilizar el `MediaPlayer` instancia sin los gastos generales de liberación de recursos, recreando la `MediaPlayer`y la reasignación de recursos.

* Si la variable `MediaPlayer` está en estado ERROR y debe borrarse.

   >[!IMPORTANT]
   >
   >Esta es la única manera de recuperarse del estado ERROR.

1. Llamada `reset` para devolver el `MediaPlayer` a su estado sin inicializar:

   ```java
   void reset() throws IllegalStateException; 
   ```

1. Uso `MediaPlayer.replaceCurrentResource` para cargar otro `MediaResource`.

   >[!TIP]
   >
   >Para borrar un error, cargue el mismo `MediaResource`.

1. Cuando reciba la `STATUS_CHANGED` Llamada de retorno del evento con el estado PREPARADO, inicie la reproducción.

## Lanzamiento de una instancia de MediaPlayer y recursos{#release-a-mediaplayer-instance-and-resources}

Debe liberar una instancia de MediaPlayer y recursos cuando ya no necesite MediaResource.

Cuando libera un `MediaPlayer` , los recursos de hardware subyacentes asociados a este objeto `MediaPlayer` objeto están desasignados.

Estas son algunas razones para lanzar un MediaPlayer:

* Mantener recursos innecesarios puede afectar al rendimiento.
* Dejando un elemento innecesario `MediaPlayer` Este objeto puede consumir continuamente baterías para dispositivos móviles.
* Si no se admiten varias instancias del mismo códec de vídeo en un dispositivo, puede producirse un error de reproducción en otras aplicaciones.

1. Suelte el `MediaPlayer`.

   ```java
   void release() throws IllegalStateException;
   ```

Después del `MediaPlayer` Una vez liberada, ya no puede utilizarla. Si hay algún método del `MediaPlayer` se llama a la interfaz de después de su lanzamiento, y `IllegalStateException` se ha lanzado.
