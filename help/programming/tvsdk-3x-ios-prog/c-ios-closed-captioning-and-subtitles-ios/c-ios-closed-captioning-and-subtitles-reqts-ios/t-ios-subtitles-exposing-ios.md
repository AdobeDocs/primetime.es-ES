---
description: El TVSDK notifica al cliente del reproductor acerca de la disponibilidad de la variable interna AVAsset availableMediaCharacterficationsWithMediaSelectionOptions mediante la notificación PTMediaPlayerMediaSelectionOptionsAvailableNotification.
seo-description: El TVSDK notifica al cliente del reproductor acerca de la disponibilidad de la variable interna AVAsset availableMediaCharacterficationsWithMediaSelectionOptions mediante la notificación PTMediaPlayerMediaSelectionOptionsAvailableNotification.
seo-title: Exponer subtítulos
title: Exponer subtítulos
uuid: 1cd8761f-6e6f-4017-9852-fa61f36197c5
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
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

   Para obtener información sobre las pistas de audio alternativas, consulte [Audio alternativo](../../alternate-audio/ios-3x-alternate-audio.md).