---
description: Para recibir notificaciones sobre etiquetas en el manifiesto, implemente los oyentes de notificación correspondientes.
title: Agregar oyentes para notificaciones de metadatos temporizados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# Agregar oyentes para notificaciones de metadatos temporizadas {#add-listeners-for-timed-metadata-notifications}

Para recibir notificaciones sobre etiquetas en el manifiesto, implemente los oyentes de notificación correspondientes.

Puede monitorizar los metadatos temporizados escuchando los siguientes eventos, que notifican a la aplicación de la actividad relacionada:

* `PTTimedMetadataChangedNotification`: Cada vez que se identifica una etiqueta suscrita única durante el análisis del contenido, TVSDK prepara un nuevo  `PTTimedMetadata` objeto y envía esta notificación.

   El objeto contiene el nombre de la etiqueta a la que se ha suscrito, la hora local de la reproducción en la que aparecerá esta etiqueta y otros datos.

* `PTMediaPlayerTimeChangeNotification` : Para flujos en directo/lineales en los que el manifiesto/lista de reproducción se actualiza periódicamente, pueden aparecer etiquetas personalizadas adicionales en la lista de reproducción/manifiesto actualizado, por lo que se pueden agregar  `TimedMetadata` objetos adicionales a la  `MediaPlayerItem.timedMetadata` propiedad.

   Este evento notifica a la aplicación cuando esto sucede.

   Recupere los metadatos temporizados de una de las siguientes formas.

   * Configure la aplicación para que se añada como oyente a la notificación `PTTimedMetadataChangedNotification` y busque el objeto mediante `PTTimedMetadataKey`.

      ```
      [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onTimedMetadataChanged:)  
        name:PTTimedMetadataChangedNotification object:self.player.currentItem]; 
      
      - (void) onTimedMetadataChanged:(NSNotification *) notification { 
          NSDictionary *timedMetadataUserInfo = [[NSDictionary alloc]initWithDictionary: notification.userInfo]; 
          PTTimedMetadata *newTimedMetadata = [timedMetadataUserInfo objectForKey: PTTimedMetadataKey]; 
      }
      ```

   * Acceda a la propiedad `timedMetadataCollection` de `PTMediaPlayerItem`, que consta de todos los objetos `PTTimedMetadata` que se han notificado hasta el momento.