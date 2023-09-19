---
description: Instant-on precarga partes del contenido en uno o más canales. Una vez que el usuario selecciona o cambia de canal, el contenido comienza antes porque parte del almacenamiento en búfer ya se ha completado.
title: Instant-on
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Instant-on{#instant-on}

Instant-on precarga partes del contenido en uno o más canales. Una vez que el usuario selecciona o cambia de canal, el contenido comienza antes porque parte del almacenamiento en búfer ya se ha completado.

Cuando el reproductor esté en la `PTMediaPlayerStatusReady` estado, llamada `prepareToPlay` para precargar y procesar parte del contenido para su posterior reproducción.

>[!TIP]
>
>Si no llama a `prepareToPlay`, llamando a `play` llama automáticamente a `prepareToPlay` primero. La precarga y el procesamiento se completan en este momento.

TVSDK completa algunas o todas las tareas siguientes para `prepareToPlay`:

* Si la clave de metadatos `kSyncCookiesWithAVAsset` , TVSDK realiza una solicitud al archivo M3U8 original para sincronizar las cookies.
* Carga claves de metadatos DRM.
* Crea y prepara algunas estructuras, elementos o recursos necesarios para reproducir contenido.

>[!TIP]
>
>El `PTMediaPlayer` y `PTMediaPlayerItem` `prepareToPlay` Los métodos de son iguales. Para evitar la creación de un `PTMediaPlayer` para cada recurso, utilice la variable `PTMediaPlayerItem` método.

Instant-on le ayuda a iniciar varias instancias del reproductor de medios, o instancias del cargador de elementos del reproductor de medios, simultáneamente en segundo plano y en las transmisiones de vídeo de búfer en todas estas instancias. Cuando un usuario cambia el canal y el flujo se ha almacenado en búfer correctamente, llamando a `play` en el nuevo canal, la reproducción comienza antes.
