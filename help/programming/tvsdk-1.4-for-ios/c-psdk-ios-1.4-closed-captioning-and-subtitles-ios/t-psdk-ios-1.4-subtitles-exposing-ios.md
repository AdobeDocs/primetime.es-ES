---
description: El TVSDK notifica al cliente del reproductor sobre la disponibilidad de las variables AVAsset disponiblesMediaCharacteristicWithMediaSelectionOptions internas mediante la notificación PTMediaPlayerMediaSelectionOptionsAvailableNotification.
title: Exponer subtítulos
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# Exponer subtítulos {#expose-subtitles}

El TVSDK notifica al cliente del reproductor sobre la disponibilidad de las variables AVAsset disponiblesMediaCharacteristicWithMediaSelectionOptions internas mediante la notificación PTMediaPlayerMediaSelectionOptionsAvailableNotification.

Puede acceder a los subtítulos disponibles a través del `PTMediaPlayerItem` propiedad de `subtitlesOptions`.

Para exponer subtítulos:

1. Registre el cliente como oyente para el `PTMediaPlayerMediaSelectionOptionsAvailableNotification` notificación.

   ```
   [[NSNotificationCenter defaultCenter]  
     addObserver:self selector:@selector(onMediaPlayerItemMediaSelectionOptionsAvailable:)  
     name:PTMediaPlayerMediaSelectionOptionsAvailableNotification object:self.player];
   ```

   Cuando el cliente reciba esta notificación, los subtítulos estarán listos en la `PTMediaPlayerItem`.
1. Implementación de `onMediaPlayerItemMediaSelectionOptionsAvailable` método similar al siguiente ejemplo:

   ```
   - (void) onMediaPlayerItemMediaSelectionOptionsAvailable:(NSNotification *) notification { 
       NSArray* subtitlesOptions = self.player.currentItem.subtitlesOptions; 
       NSArray* audioOptions = self.player.currentItem.audioOptions; 
   }
   ```

   Para obtener información sobre pistas de audio alternativas, consulte  [Audio alternativo](../alternate-audio/c-psdk-ios-1.4-alternate-audio.md).
