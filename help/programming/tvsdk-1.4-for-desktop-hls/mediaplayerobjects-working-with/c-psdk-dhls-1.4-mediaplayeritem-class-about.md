---
description: El objeto MediaPlayer representa el reproductor multimedia. Un MediaPlayerItem representa el audio o el vídeo en el reproductor.
title: Acerca de la clase MediaPlayerItem
exl-id: ff7011ae-57d7-41e1-98be-5319bdc6f799
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 0%

---

# Acerca de la clase MediaPlayerItem{#about-the-mediaplayeritem-class}

El objeto MediaPlayer representa el reproductor multimedia. Un MediaPlayerItem representa el audio o el vídeo en el reproductor.

<!--<a id="section_01BC89E5C5A94D0A95EF9D29FBCE758A"></a>-->

Una vez que un recurso multimedia se ha cargado correctamente, TVSDK crea una instancia de la variable `MediaPlayerItem` para proporcionar acceso a ese recurso.

El `MediaResource` representa una solicitud emitida por la capa de aplicación al `MediaPlayer` para cargar contenido.

El `MediaPlayer` resuelve el recurso multimedia, carga el archivo de manifiesto asociado y analiza el manifiesto. Esta es la parte asíncrona del proceso de carga de recursos. El `MediaPlayerItem` La instancia se genera después de que se haya resuelto el recurso y esta instancia es una versión resuelta de un `MediaResource`. TVSDK proporciona acceso a los recién creados `MediaPlayerItem` instancia a través de `MediaPlayer.currentItem`.

>[!TIP]
>
>Debe esperar a que el recurso se cargue correctamente antes de acceder al elemento del reproductor de medios.
