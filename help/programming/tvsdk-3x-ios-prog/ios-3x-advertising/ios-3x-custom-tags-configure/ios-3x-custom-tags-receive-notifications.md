---
description: Para recibir notificaciones sobre las etiquetas en el manifiesto, implemente los oyentes de notificaciones adecuados.
title: Añadir oyentes para notificaciones de metadatos cronometradas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# Añadir oyentes para notificaciones de metadatos cronometradas {#add-listeners-for-timed-metadata-notifications}

Para recibir notificaciones sobre las etiquetas en el manifiesto, implemente los oyentes de notificaciones adecuados.

Puede monitorizar los metadatos cronometrados si escucha los siguientes eventos, que notifican a la aplicación la actividad relacionada:

* `PTTimedMetadataChangedNotification`: Cada vez que se identifica una etiqueta suscrita única durante el análisis del contenido, TVSDK prepara una nueva `PTTimedMetadata` y envía esta notificación.

  El objeto contiene el nombre de la etiqueta a la que se ha suscrito, la hora local de la reproducción en la que aparecerá esta etiqueta y otros datos.

* `PTMediaPlayerTimeChangeNotification` : Para emisiones lineales/en directo en las que el manifiesto/lista de reproducción se actualiza periódicamente, es posible que aparezcan etiquetas personalizadas adicionales en la lista de reproducción/manifiesto actualizado, por lo que resulta `TimedMetadata` objetos que se pueden añadir a `MediaPlayerItem.timedMetadata` propiedad.

  Este evento notifica a la aplicación cuando esto sucede.

  Recupere los metadatos cronometrados de una de las siguientes maneras.

   * Configure la aplicación para que se agregue como oyente al `PTTimedMetadataChangedNotification` notificación y recuperación del objeto mediante `PTTimedMetadataKey`.

     ```
     [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onTimedMetadataChanged:)  
       name:PTTimedMetadataChangedNotification object:self.player.currentItem]; 
     
     - (void) onTimedMetadataChanged:(NSNotification *) notification { 
         NSDictionary *timedMetadataUserInfo = [[NSDictionary alloc]initWithDictionary: notification.userInfo]; 
         PTTimedMetadata *newTimedMetadata = [timedMetadataUserInfo objectForKey: PTTimedMetadataKey]; 
     }
     ```

   * Acceda a la `timedMetadataCollection` propiedad de `PTMediaPlayerItem`, que consta de todos los `PTTimedMetadata` objetos que se han notificado hasta ahora.
