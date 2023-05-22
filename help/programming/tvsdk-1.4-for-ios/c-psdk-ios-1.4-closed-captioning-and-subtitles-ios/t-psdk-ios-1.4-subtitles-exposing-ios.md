---
description: El TVSDK notifica al cliente del reproductor sobre la disponibilidad de las variables AVAsset disponiblesMediaCharacteristicWithMediaSelectionOptions internas mediante la notificación PTMediaPlayerMediaSelectionOptionsAvailableNotification.
title: Exponer subtítulos
exl-id: dc726a5b-2eab-4ebd-8773-7396bf818205
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
