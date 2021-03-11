---
description: La precarga instantánea de partes del contenido multimedia en uno o varios canales. Después de que un usuario selecciona o cambia de canal, el contenido se inicia antes porque parte del almacenamiento en búfer ya se ha completado.
title: Instantáneo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# Instantáneo {#instant-on}

La precarga instantánea de partes del contenido multimedia en uno o varios canales. Después de que un usuario selecciona o cambia de canal, el contenido se inicia antes porque parte del almacenamiento en búfer ya se ha completado.

Cuando el reproductor esté en estado `PTMediaPlayerStatusReady`, llame a `prepareToPlay` para cargar previamente y procesar parte del contenido para una reproducción posterior.

>[!TIP]
>
>Si no llama a `prepareToPlay`, llamar a `play` automáticamente llama `prepareToPlay` primero. La precarga y el procesamiento se completan en este momento.

TVSDK completa algunas o todas las tareas siguientes para `prepareToPlay`:

* Si la clave de metadatos `kSyncCookiesWithAVAsset` está establecida, TVSDK realiza una solicitud al archivo M3U8 original para sincronizar las cookies.
* Carga las claves de metadatos DRM.
* Crea y prepara algunas estructuras, elementos o recursos necesarios para reproducir contenido.

>[!TIP]
>
>Los métodos `PTMediaPlayer` y `PTMediaPlayerItem` `prepareToPlay` son iguales. Para evitar crear una instancia `PTMediaPlayer` independiente para cada recurso, utilice el método `PTMediaPlayerItem`.

La función Instant-on le ayuda a iniciar varias instancias de reproductor de medios o instancias de cargador de elementos de reproductor de medios simultáneamente en los flujos de vídeo de búfer y en segundo plano en todas estas instancias. Cuando un usuario cambia el canal y el flujo se almacena en búfer correctamente, al llamar a `play` en el nuevo canal, se inicia la reproducción antes.