---
description: Después de cargar correctamente el objeto MediaResource, TVSDK crea una instancia de la clase MediaPlayerItem para proporcionar acceso a ese recurso.
seo-description: Después de cargar correctamente el objeto MediaResource, TVSDK crea una instancia de la clase MediaPlayerItem para proporcionar acceso a ese recurso.
seo-title: Acerca de la clase MediaPlayerItem
title: Acerca de la clase MediaPlayerItem
uuid: 2d37f358-d158-481b-81d5-27546e9c2e0e
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Acerca de la clase MediaPlayerItem {#about-the-mediaplayeritem-class}

El objeto MediaPlayer representa el reproductor multimedia. MediaPlayerItem representa audio o vídeo en el reproductor.

Después de cargar correctamente el objeto MediaResource, TVSDK crea una instancia de la clase MediaPlayerItem para proporcionar acceso a ese recurso.

El `MediaResource` representa una solicitud emitida por la capa de la aplicación a la `MediaPlayer` instancia para cargar contenido.

El `MediaPlayer` resuelve el recurso de medios, carga el archivo de manifiesto asociado y analiza el manifiesto. Es la parte asincrónica del proceso de carga de recursos. La `MediaPlayerItem` instancia se produce después de que se haya resuelto el recurso y esta instancia es una versión resuelta de un `MediaResource`. TVSDK proporciona acceso a la `MediaPlayerItem` instancia recién creada a través de `MediaPlayer.CurrentItem`.

>[!TIP]
>
>Debe esperar a que el recurso se cargue correctamente antes de acceder al elemento del reproductor multimedia.