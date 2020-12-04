---
description: El TVSDK notifica al cliente del reproductor acerca de la disponibilidad de la variable interna AVAsset availableMediaCharacterficationsWithMediaSelectionOptions mediante la notificación PTMediaPlayerMediaSelectionOptionsAvailableNotification.
seo-description: El TVSDK notifica al cliente del reproductor acerca de la disponibilidad de la variable interna AVAsset availableMediaCharacterficationsWithMediaSelectionOptions mediante la notificación PTMediaPlayerMediaSelectionOptionsAvailableNotification.
seo-title: Exponer subtítulos
title: Exponer subtítulos
uuid: 657ab9c7-b205-4d13-81a7-51bc8e7d5ee2
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 0%

---


# Exponer subtítulos {#expose-subtitles}

El TVSDK notifica al cliente del reproductor acerca de la disponibilidad de la variable interna AVAsset availableMediaCharacterficationsWithMediaSelectionOptions mediante la notificación PTMediaPlayerMediaSelectionOptionsAvailableNotification.

Puede acceder a los subtítulos disponibles a través de la propiedad `PTMediaPlayerItem` `subtitlesOptions`.

Para exponer subtítulos:

1. Registre el cliente como oyente para la notificación `PTMediaPlayerMediaSelectionOptionsAvailableNotification`.

   ```
   [[NSNotificationCenter defaultCenter]  
     addObserver:self selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:)  
     name:PTMediaPlayerMediaSelectionOptionsAvailableNotification object:self.player];
   ```

   Cuando su cliente recibe esta notificación, los subtítulos están listos en `PTMediaPlayerItem`.
1. Implemente el método `onMediaPlayerItemMediaSelectionOptionsAvailable` similar al siguiente ejemplo:

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

   Para obtener información sobre las pistas de audio alternativas, consulte [Audio alternativo](../alternate-audio/c-psdk-ios-1.4-alternate-audio.md).