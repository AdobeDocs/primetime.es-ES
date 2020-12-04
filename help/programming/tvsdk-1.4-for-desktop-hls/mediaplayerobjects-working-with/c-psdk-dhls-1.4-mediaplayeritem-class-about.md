---
description: El objeto MediaPlayer representa el reproductor multimedia. MediaPlayerItem representa audio o vídeo en el reproductor.
seo-description: El objeto MediaPlayer representa el reproductor multimedia. MediaPlayerItem representa audio o vídeo en el reproductor.
seo-title: Acerca de la clase MediaPlayerItem
title: Acerca de la clase MediaPlayerItem
uuid: 531dd1a6-d72c-4ae3-9c3f-2f1d854245c5
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---


# Acerca de la clase MediaPlayerItem{#about-the-mediaplayeritem-class}

El objeto MediaPlayer representa el reproductor multimedia. MediaPlayerItem representa audio o vídeo en el reproductor.

<!--<a id="section_01BC89E5C5A94D0A95EF9D29FBCE758A"></a>-->

Después de cargar correctamente un recurso multimedia, TVSDK crea una instancia de la clase `MediaPlayerItem` para proporcionar acceso a ese recurso.

El `MediaResource` representa una solicitud emitida por la capa de aplicación a la instancia `MediaPlayer` para cargar contenido.

El `MediaPlayer` resuelve el recurso de medios, carga el archivo de manifiesto asociado y analiza el manifiesto. Es la parte asincrónica del proceso de carga de recursos. La instancia `MediaPlayerItem` se produce después de que el recurso se haya resuelto y esta instancia es una versión resuelta de `MediaResource`. TVSDK proporciona acceso a la instancia `MediaPlayerItem` recién creada mediante `MediaPlayer.currentItem`.

>[!TIP]
>
>Debe esperar a que el recurso se cargue correctamente antes de acceder al elemento del reproductor multimedia.

