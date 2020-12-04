---
description: Una vez que MediaResource se ha cargado correctamente, TVSDK del explorador crea una instancia de la clase MediaPlayerItem para proporcionar acceso a ese recurso.
seo-description: Una vez que MediaResource se ha cargado correctamente, TVSDK del explorador crea una instancia de la clase MediaPlayerItem para proporcionar acceso a ese recurso.
seo-title: Acerca de la clase MediaPlayerItem
title: Acerca de la clase MediaPlayerItem
uuid: 5226d3ad-2438-44fe-a8ef-bcc0da8331b8
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---


# Acerca de la clase MediaPlayerItem{#about-the-mediaplayeritem-class}

Una vez que MediaResource se ha cargado correctamente, TVSDK del explorador crea una instancia de la clase MediaPlayerItem para proporcionar acceso a ese recurso.

El `MediaResource` representa una solicitud emitida por la capa de aplicación a la instancia `MediaPlayer` para cargar contenido.

El `MediaPlayer` resuelve el recurso de medios, carga el archivo de manifiesto asociado y analiza el manifiesto. Es la parte asincrónica del proceso de carga de recursos. La instancia `MediaPlayerItem` se produce después de que el recurso se haya resuelto y esta instancia es una versión resuelta de `MediaResource`. El SDK TVSDK del explorador proporciona acceso a la instancia `MediaPlayerItem` recién creada mediante `MediaPlayer.CurrentItem`.

>[!TIP]
>
>Debe esperar a que el recurso se cargue correctamente antes de acceder al elemento del reproductor multimedia.

