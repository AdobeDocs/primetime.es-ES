---
seo-title: Operaciones esenciales de reproducción de vídeo
title: Operaciones esenciales de reproducción de vídeo
description: PlaybackManager proporciona operaciones esenciales del flujo HLS
seo-description: PlaybackManager proporciona operaciones esenciales del flujo HLS
uuid: 7ac93f1f-9233-4462-a4be-528d1aa524a9
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---


# Operaciones esenciales de reproducción de vídeo {#essential-operations-of-video-playback}

PlaybackManager proporciona operaciones esenciales de flujo HLS:

* Invoca el [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html), que puede responder correctamente a los eventos de vídeo.
* Proporciona una operación de reproducción como reproducir, pausar y buscar.
* Devuelve la información sobre el reproductor, como el estado del reproductor, el intervalo de reproducción y el flujo de vídeo en directo.
* Determina si ABR está habilitado y establece los parámetros ABR y de control de búfer según los datos de configuración suministrados.
* Determina si el control de búfer está activado y establece los parámetros de control de búfer en función de los datos de configuración suministrados.