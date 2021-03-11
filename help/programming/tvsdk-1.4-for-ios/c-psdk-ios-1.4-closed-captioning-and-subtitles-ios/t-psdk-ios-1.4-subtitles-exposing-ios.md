---
description: El TVSDK notifica al cliente del reproductor acerca de la disponibilidad de availableMediaCharacterficationsWithMediaSelectionOptions del grupo AVAset interno mediante la notificación PTMediaPlayerMediaSelectionOptionsAvailableNotification.
title: Exponer subtítulos
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# Exponer subtítulos {#expose-subtitles}

El TVSDK notifica al cliente del reproductor acerca de la disponibilidad de availableMediaCharacterficationsWithMediaSelectionOptions del grupo AVAset interno mediante la notificación PTMediaPlayerMediaSelectionOptionsAvailableNotification.

Puede acceder a los subtítulos disponibles a través de la propiedad `PTMediaPlayerItem` `subtitlesOptions`.

Para exponer subtítulos:

1. Registre el cliente como oyente para la notificación `PTMediaPlayerMediaSelectionOptionsAvailableNotification`.

   ```
   [[NSNotificationCenter defaultCenter]  
     addObserver:self selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:)  
     name:PTMediaPlayerMediaSelectionOptionsAvailableNotification object:self.player];
   ```

   Cuando el cliente recibe esta notificación, los subtítulos están listos en `PTMediaPlayerItem`.
1. Implemente el método `onMediaPlayerItemMediaSelectionOptionsAvailable` de forma similar al siguiente ejemplo:

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

   Para obtener información sobre pistas de audio alternativas, consulte [Audio alternativo](../alternate-audio/c-psdk-ios-1.4-alternate-audio.md).