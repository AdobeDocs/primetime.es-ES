---
description: Una vez que MediaResource se ha cargado correctamente, el TVSDK del explorador crea una instancia de la clase MediaPlayerItem para proporcionar acceso a ese recurso.
title: Acerca de la clase MediaPlayerItem
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---

# Acerca de la clase MediaPlayerItem{#about-the-mediaplayeritem-class}

Una vez que MediaResource se ha cargado correctamente, el TVSDK del explorador crea una instancia de la clase MediaPlayerItem para proporcionar acceso a ese recurso.

El `MediaResource` representa una solicitud emitida por la capa de aplicación al `MediaPlayer` para cargar contenido.

El `MediaPlayer` resuelve el recurso multimedia, carga el archivo de manifiesto asociado y analiza el manifiesto. Esta es la parte asíncrona del proceso de carga de recursos. El `MediaPlayerItem` La instancia se genera después de que se haya resuelto el recurso y esta instancia es una versión resuelta de un `MediaResource`. El TVSDK del explorador proporciona acceso al recién creado `MediaPlayerItem` instancia a través de `MediaPlayer.CurrentItem`.

>[!TIP]
>
>Debe esperar a que el recurso se cargue correctamente antes de acceder al elemento del reproductor de medios.
