---
description: El objeto MediaPlayer representa el reproductor multimedia. MediaPlayerItem representa audio o vídeo en el reproductor.
seo-description: El objeto MediaPlayer representa el reproductor multimedia. MediaPlayerItem representa audio o vídeo en el reproductor.
seo-title: Acerca de la clase MediaPlayerItem
title: Acerca de la clase MediaPlayerItem
uuid: d7f65edf-4693-4b1e-bae0-46fadce98751
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Acerca de la clase MediaPlayerItem{#about-the-mediaplayeritem-class}

El objeto MediaPlayer representa el reproductor multimedia. MediaPlayerItem representa audio o vídeo en el reproductor.

Después de cargar correctamente un recurso multimedia, TVSDK crea una instancia de la `MediaPlayerItem` clase para proporcionar acceso a dicho recurso.

El `MediaResource` representa una solicitud emitida por la capa de la aplicación a la `MediaPlayer` instancia para cargar contenido.

El `MediaPlayer` resuelve el recurso de medios, carga el archivo de manifiesto asociado y analiza el manifiesto. Es la parte asincrónica del proceso de carga de recursos. La `MediaPlayerItem` instancia se produce después de que se haya resuelto el recurso y esta instancia es una versión resuelta de un `MediaResource`. TVSDK proporciona acceso a la `MediaPlayerItem` instancia recién creada mediante `MediaPlayer.CurrentItem`

>[!TIP]
>
>Debe esperar a que el recurso se cargue correctamente antes de acceder al elemento del reproductor multimedia.

