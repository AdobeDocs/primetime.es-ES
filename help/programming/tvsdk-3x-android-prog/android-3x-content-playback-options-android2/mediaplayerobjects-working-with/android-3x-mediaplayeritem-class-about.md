---
description: Después de cargar correctamente el objeto MediaResource, TVSDK crea una instancia de la clase MediaPlayerItem para proporcionar acceso a ese recurso.
seo-description: Después de cargar correctamente el objeto MediaResource, TVSDK crea una instancia de la clase MediaPlayerItem para proporcionar acceso a ese recurso.
seo-title: Acerca de la clase MediaPlayerItem
title: Acerca de la clase MediaPlayerItem
uuid: fc79c442-2e38-48c4-8ef9-6dce9ad6790a
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---


# Acerca de la clase MediaPlayerItem {#about-the-mediaplayeritem-class}

El objeto MediaPlayer representa el reproductor multimedia. MediaPlayerItem representa audio o vídeo en el reproductor.

Después de cargar correctamente el objeto MediaResource, TVSDK crea una instancia de la clase MediaPlayerItem para proporcionar acceso a ese recurso.

El `MediaResource` representa una solicitud emitida por la capa de aplicación a la instancia `MediaPlayer` para cargar contenido.

El `MediaPlayer` resuelve el recurso de medios, carga el archivo de manifiesto asociado y analiza el manifiesto. Es la parte asincrónica del proceso de carga de recursos. La instancia `MediaPlayerItem` se produce después de que el recurso se haya resuelto y esta instancia es una versión resuelta de `MediaResource`. TVSDK proporciona acceso a la instancia `MediaPlayerItem` recién creada mediante `MediaPlayer.CurrentItem`.

>[!TIP]
>
>Debe esperar a que el recurso se cargue correctamente antes de acceder al elemento del reproductor multimedia.