---
description: Puede restablecer, reutilizar o liberar una instancia de MediaPlayer que ya no necesite.
seo-description: Puede restablecer, reutilizar o liberar una instancia de MediaPlayer que ya no necesite.
seo-title: Reutilización o eliminación de una instancia de MediaPlayer
title: Reutilización o eliminación de una instancia de MediaPlayer
uuid: da7b3468-3f0f-4025-927b-d47764a053af
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---


# Reutilizar o quitar una instancia de MediaPlayer {#reuse-or-remove-a-mediaplayer-instance}

Puede restablecer, reutilizar o liberar una instancia de MediaPlayer que ya no necesite.

## Restablecer o reutilizar una instancia de MediaPlayer {#section_E6A2446A2D0B4ACD9EA980685B2E57D9}

Al restablecer una instancia `MediaPlayer`, se devuelve a su estado IDLE no inicializado tal como se define en `MediaPlayerStatus`

* Desea reutilizar una instancia `MediaPlayer` pero necesita cargar un nuevo `MediaResource` (contenido de vídeo) y reemplazar la instancia anterior.

   Restablecer le permite reutilizar la instancia `MediaPlayer` sin necesidad de aprovechar la sobrecarga de liberar recursos, volver a crear `MediaPlayer` y reasignar recursos.

* Cuando `MediaPlayer` está en estado ERROR y debe borrarse.

   >[!IMPORTANT]
   >
   >Esta es la única manera de recuperarse del estado ERROR.

   1. Llame a `reset` para devolver la instancia `MediaPlayer` a su estado no inicializado:

      ```java
      void reset() throws MediaPlayerException; 
      ```

   1. Utilice `MediaPlayer.replaceCurrentResource()` para cargar otro `MediaResource`.

      >[!NOTE]
      >
      >Para borrar un error, cargue el mismo `MediaResource`.

   1. Cuando reciba la rellamada de `STATUS_CHANGED` evento con el estado `PREPARED`, inicio la reproducción.

## Liberar una instancia y recursos de MediaPlayer {#section_13A0914AFF784943ABC343F7EB249C4E}

Debe liberar una instancia `MediaPlayer` y recursos cuando ya no necesite el `MediaResource`.

Cuando libera un objeto `MediaPlayer`, se desasignan los recursos de hardware subyacentes asociados a este objeto `MediaPlayer`.

A continuación se indican algunas razones para lanzar un `MediaPlayer`:

* La retención de recursos innecesarios puede afectar al rendimiento.
* Si se deja un objeto innecesario `MediaPlayer` creado como instancia, puede producirse un consumo continuo de la batería para dispositivos móviles.
* Si no se admiten varias instancias del mismo códec de vídeo en un dispositivo, es posible que se produzca un error de reproducción en otras aplicaciones.

* Libere el `MediaPlayer`.

   ```java
   void release() throws MediaPlayerException;
   ```

   >[!NOTE]
   >
   >Una vez liberada la instancia `MediaPlayer`, ya no podrá usarla. Si se llama a algún método de la interfaz `MediaPlayer` después de liberarlo, se genera un `MediaPlayerException`.