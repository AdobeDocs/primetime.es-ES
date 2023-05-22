---
description: Una vez que MediaResource se ha cargado correctamente, el TVSDK del explorador crea una instancia de la clase MediaPlayerItem para proporcionar acceso a ese recurso.
title: Acerca de la clase MediaPlayerItem
exl-id: 6e47914c-3d46-4aaf-9144-1a00d886e5bf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
