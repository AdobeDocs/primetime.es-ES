---
title: Operaciones esenciales de reproducción de vídeo
description: PlaybackManager proporciona operaciones esenciales de transmisión HLS
exl-id: b4d1b41a-7a16-47f5-be88-6b52f0451813
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
