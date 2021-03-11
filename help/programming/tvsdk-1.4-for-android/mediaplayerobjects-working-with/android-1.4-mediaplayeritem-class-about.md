---
description: El objeto MediaPlayer representa el reproductor multimedia. MediaPlayerItem representa audio o vídeo en el reproductor.
title: Acerca de la clase MediaPlayerItem
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---


# Acerca de la clase MediaPlayerItem{#about-the-mediaplayeritem-class}

El objeto MediaPlayer representa el reproductor multimedia. MediaPlayerItem representa audio o vídeo en el reproductor.

Una vez cargado correctamente un recurso de medios, TVSDK crea una instancia de la clase `MediaPlayerItem` para proporcionar acceso a ese recurso.

El `MediaResource` representa una solicitud que emite la capa de aplicación a la instancia `MediaPlayer` para cargar contenido.

El `MediaPlayer` resuelve el recurso de medios, carga el archivo de manifiesto asociado y analiza el manifiesto. Esta es la parte asíncrona del proceso de carga de recursos. La instancia `MediaPlayerItem` se produce después de que el recurso se haya resuelto y esta instancia es una versión resuelta de `MediaResource`. TVSDK proporciona acceso a la instancia `MediaPlayerItem` recién creada a través de `MediaPlayer.CurrentItem`

>[!TIP]
>
>Debe esperar a que el recurso se cargue correctamente antes de acceder al elemento del reproductor de contenidos.

