---
title: Operaciones esenciales de reproducción de vídeo
description: PlaybackManager proporciona operaciones esenciales de transmisión HLS
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# Operaciones esenciales de reproducción de vídeo {#essential-operations-of-video-playback}

PlaybackManager proporciona operaciones esenciales de flujo HLS:

* Invoca el [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html), que puede responder correctamente a eventos de vídeo.
* Proporciona operaciones de reproducción, como reproducción, pausa y búsqueda.
* Devuelve la información sobre el reproductor, como el estado del reproductor, el intervalo de reproducción y el flujo de vídeo en directo.
* Determina si ABR está habilitado y establece los parámetros de control ABR y búfer en función de los datos de configuración suministrados.
* Determina si el control de búfer está habilitado y establece los parámetros de control de búfer según los datos de configuración proporcionados.
