---
description: Para recibir notificaciones sobre etiquetas en el manifiesto, implemente los oyentes de notificación correspondientes.
seo-description: Para recibir notificaciones sobre etiquetas en el manifiesto, implemente los oyentes de notificación correspondientes.
seo-title: Adición de oyentes para notificaciones de metadatos temporizados
title: Adición de oyentes para notificaciones de metadatos temporizados
uuid: b6939011-a6ff-4342-8e7c-3a0c805ee91c
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Adición de oyentes para notificaciones de metadatos temporizados {#add-listeners-for-timed-metadata-notifications}

Para recibir notificaciones sobre etiquetas en el manifiesto, implemente los oyentes de notificación correspondientes.

Puede supervisar los metadatos temporizados escuchando los siguientes eventos, que notifican a la aplicación la actividad relacionada:

* `PTTimedMetadataChangedNotification`:: Cada vez que se identifica una etiqueta suscrita única durante el análisis del contenido, TVSDK prepara un nuevo `PTTimedMetadata` objeto y envía esta notificación.

   El objeto contiene el nombre de la etiqueta a la que se suscribió, la hora local de la reproducción en la que aparecerá esta etiqueta y otros datos.

* `PTMediaPlayerTimeChangeNotification` :: En el caso de flujos en directo/lineales en los que el manifiesto/lista de reproducción se actualiza periódicamente, es posible que aparezcan etiquetas personalizadas adicionales en la lista de reproducción/manifiesto actualizado, por lo que se pueden agregar `TimedMetadata` objetos adicionales a la `MediaPlayerItem.timedMetadata` propiedad.

   Este evento notifica a la aplicación cuando esto sucede.

   Recupere los metadatos temporizados de una de las siguientes formas.

   * Configure la aplicación para que se añada como un detector a la notificación y `PTTimedMetadataChangedNotification` busque el objeto mediante `PTTimedMetadataKey`.

      ```
      [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onTimedMetadataChanged:)  
        name:PTTimedMetadataChangedNotification object:self.player.currentItem]; 
      
      - (void) onTimedMetadataChanged:(NSNotification *) notification { 
          NSDictionary *timedMetadataUserInfo = [[NSDictionary alloc]initWithDictionary: notification.userInfo]; 
          PTTimedMetadata *newTimedMetadata = [timedMetadataUserInfo objectForKey: PTTimedMetadataKey]; 
      }
      ```

   * Acceda a la `timedMetadataCollection` propiedad de `PTMediaPlayerItem`, que consta de todos los `PTTimedMetadata` objetos notificados hasta ahora.