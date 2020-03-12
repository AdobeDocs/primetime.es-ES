---
description: Después de cargar correctamente el objeto MediaResource, TVSDK crea una instancia de la clase MediaPlayerItem para proporcionar acceso a ese recurso.
seo-description: Después de cargar correctamente el objeto MediaResource, TVSDK crea una instancia de la clase MediaPlayerItem para proporcionar acceso a ese recurso.
seo-title: Acerca de la clase MediaPlayerItem
title: Acerca de la clase MediaPlayerItem
uuid: fc79c442-2e38-48c4-8ef9-6dce9ad6790a
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Acerca de la clase MediaPlayerItem {#about-the-mediaplayeritem-class}

El objeto MediaPlayer representa el reproductor multimedia. MediaPlayerItem representa audio o vídeo en el reproductor.

Después de cargar correctamente el objeto MediaResource, TVSDK crea una instancia de la clase MediaPlayerItem para proporcionar acceso a ese recurso.

El `MediaResource` representa una solicitud emitida por la capa de la aplicación a la `MediaPlayer` instancia para cargar contenido.

El `MediaPlayer` resuelve el recurso de medios, carga el archivo de manifiesto asociado y analiza el manifiesto. Es la parte asincrónica del proceso de carga de recursos. La `MediaPlayerItem` instancia se produce después de que se haya resuelto el recurso y esta instancia es una versión resuelta de un `MediaResource`. TVSDK proporciona acceso a la `MediaPlayerItem` instancia recién creada a través de `MediaPlayer.CurrentItem`.

>[!TIP]
>
>Debe esperar a que el recurso se cargue correctamente antes de acceder al elemento del reproductor multimedia.