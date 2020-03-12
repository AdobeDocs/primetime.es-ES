---
description: La precarga instantánea de partes del medio en uno o varios canales. Una vez que un usuario selecciona o cambia los canales, el contenido comienza antes porque ya se ha completado parte del almacenamiento en búfer.
seo-description: La precarga instantánea de partes del medio en uno o varios canales. Una vez que un usuario selecciona o cambia los canales, el contenido comienza antes porque ya se ha completado parte del almacenamiento en búfer.
seo-title: Instantáneo
title: Instantáneo
uuid: 98a5ef79-51e4-474e-a6e8-ca449c430b5e
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Instantáneo {#instant-on}

La precarga instantánea de partes del medio en uno o varios canales. Una vez que un usuario selecciona o cambia los canales, el contenido comienza antes porque ya se ha completado parte del almacenamiento en búfer.

Cuando el reproductor esté en el `PTMediaPlayerStatusReady` estado, llame `prepareToPlay` para cargar previamente y procesar parte del contenido para una reproducción posterior.

>[!TIP]
>
>Si no llama `prepareToPlay`, llama `play` automáticamente primero a `prepareToPlay` . La precarga y el procesamiento se completan en este momento.

TVSDK completa algunas o todas las siguientes tareas para `prepareToPlay`:

* Si la clave de metadatos `kSyncCookiesWithAVAsset` está configurada, TVSDK realiza una solicitud al archivo M3U8 original para sincronizar las cookies.
* Carga las claves de metadatos DRM.
* Crea y prepara algunas estructuras, elementos o recursos necesarios para reproducir contenido.

>[!TIP]
>
>Los `PTMediaPlayer` métodos y `PTMediaPlayerItem``prepareToPlay` son iguales. Para evitar crear una `PTMediaPlayer` instancia independiente para cada recurso, utilice el `PTMediaPlayerItem` método .

Instantáneo ayuda a iniciar varias instancias de reproductor de medios o instancias de cargador de elementos de reproductor de medios simultáneamente en segundo plano y en almacenar en búfer los flujos de vídeo en todas estas instancias. Cuando un usuario cambia el canal y el flujo se almacena en el búfer correctamente, al llamar `play` al nuevo canal se inicia la reproducción antes.