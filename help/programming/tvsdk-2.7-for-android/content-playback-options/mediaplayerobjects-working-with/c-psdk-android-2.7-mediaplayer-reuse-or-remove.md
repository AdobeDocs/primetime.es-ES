---
description: Puede restablecer, reutilizar o liberar una instancia de MediaPlayer que ya no necesite.
title: Reutilización o eliminación de una instancia de MediaPlayer
exl-id: 1ee25dd0-95e6-472d-b80c-ef9d8461302d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Reutilización o eliminación de una instancia de MediaPlayer {#reuse-or-remove-a-mediaplayer-instance}

Puede restablecer, reutilizar o liberar una instancia de MediaPlayer que ya no necesite.

## Restablecer o reutilizar una instancia de MediaPlayer {#section_E6A2446A2D0B4ACD9EA980685B2E57D9}

Cuando restablece un `MediaPlayer` instancia, se devuelve a su estado IDLE sin inicializar tal como se define en `MediaPlayerStatus`

* Desea volver a utilizar un `MediaPlayer` instancia, pero debe cargar una nueva `MediaResource` (contenido de vídeo) y reemplace la instancia anterior.

   El restablecimiento le permite reutilizar el `MediaPlayer` instancia sin los gastos generales de liberación de recursos, recreando la `MediaPlayer`y la reasignación de recursos.

* Si la variable `MediaPlayer` está en estado ERROR y debe borrarse.

   >[!IMPORTANT]
   >
   >Esta es la única manera de recuperarse del estado de ERROR.

   1. Llamada `reset` para devolver el `MediaPlayer` a su estado sin inicializar:

      ```java
      void reset() throws MediaPlayerException; 
      ```

   1. Uso `MediaPlayer.replaceCurrentResource()` para cargar otro `MediaResource`.

      >[!NOTE]
      >
      >Para borrar un error, cargue el mismo `MediaResource`.

   1. Cuando reciba la `STATUS_CHANGED` devolución de llamada de evento con `PREPARED` estado, inicie la reproducción.

## Lanzamiento de una instancia de MediaPlayer y recursos {#section_13A0914AFF784943ABC343F7EB249C4E}

Debe publicar un `MediaPlayer` y recursos cuando ya no necesite el `MediaResource`.

Cuando libera un `MediaPlayer` , los recursos de hardware subyacentes asociados a este objeto `MediaPlayer` objeto están desasignados.

Estas son algunas razones para publicar un `MediaPlayer`:

* Mantener recursos innecesarios puede afectar al rendimiento.
* Dejando un elemento innecesario `MediaPlayer` La creación de instancias de un objeto puede provocar un consumo continuo de batería para dispositivos móviles.
* Si no se admiten varias instancias del mismo códec de vídeo en un dispositivo, puede producirse un error de reproducción en otras aplicaciones.

* Suelte el `MediaPlayer`.

   ```java
   void release() throws MediaPlayerException;
   ```

   >[!NOTE]
   >
   >Después del `MediaPlayer` Una vez liberada, ya no puede utilizarla. Si hay algún método del `MediaPlayer` se llama a la interfaz de después de su lanzamiento, un `MediaPlayerException` se ha lanzado.
