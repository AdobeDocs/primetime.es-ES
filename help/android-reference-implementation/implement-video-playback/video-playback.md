---
title: Operaciones esenciales de reproducción de vídeo
description: PlaybackManager proporciona operaciones esenciales de transmisión por secuencias HLS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# Operaciones esenciales de reproducción de vídeo {#essential-operations-of-video-playback}

PlaybackManager proporciona operaciones esenciales del flujo HLS:

* Invoca el [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html), que puede responder adecuadamente a los eventos de vídeo.
* Proporciona una operación de reproducción como reproducción, pausa y búsqueda.
* Devuelve la información sobre el reproductor, como el estado del reproductor, el intervalo de reproducción y el flujo de vídeo en directo.
* Determina si ABR está habilitado y establece los parámetros ABR y buffer control según los datos de configuración suministrados.
* Determina si el control de búfer está habilitado y establece los parámetros de control de búfer según los datos de configuración suministrados.