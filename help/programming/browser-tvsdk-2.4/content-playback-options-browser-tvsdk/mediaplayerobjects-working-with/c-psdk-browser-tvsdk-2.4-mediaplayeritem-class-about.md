---
description: Una vez que MediaResource se ha cargado correctamente, TVSDK del explorador crea una instancia de la clase MediaPlayerItem para proporcionar acceso a ese recurso.
seo-description: Una vez que MediaResource se ha cargado correctamente, TVSDK del explorador crea una instancia de la clase MediaPlayerItem para proporcionar acceso a ese recurso.
seo-title: Acerca de la clase MediaPlayerItem
title: Acerca de la clase MediaPlayerItem
uuid: 5226d3ad-2438-44fe-a8ef-bcc0da8331b8
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Acerca de la clase MediaPlayerItem{#about-the-mediaplayeritem-class}

Una vez que MediaResource se ha cargado correctamente, TVSDK del explorador crea una instancia de la clase MediaPlayerItem para proporcionar acceso a ese recurso.

El `MediaResource` representa una solicitud emitida por la capa de la aplicación a la `MediaPlayer` instancia para cargar contenido.

El `MediaPlayer` resuelve el recurso de medios, carga el archivo de manifiesto asociado y analiza el manifiesto. Es la parte asincrónica del proceso de carga de recursos. La `MediaPlayerItem` instancia se produce después de que se haya resuelto el recurso y esta instancia es una versión resuelta de un `MediaResource`. El SDK de TVSDK del explorador proporciona acceso a la `MediaPlayerItem` instancia recién creada a través de `MediaPlayer.CurrentItem`.

>[!TIP]
>
>Debe esperar a que el recurso se cargue correctamente antes de acceder al elemento del reproductor multimedia.

