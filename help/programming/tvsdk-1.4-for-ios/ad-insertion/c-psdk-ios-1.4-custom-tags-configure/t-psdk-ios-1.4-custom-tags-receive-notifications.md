---
description: Para recibir notificaciones sobre etiquetas en el manifiesto, implemente los oyentes de notificación correspondientes.
seo-description: Para recibir notificaciones sobre etiquetas en el manifiesto, implemente los oyentes de notificación correspondientes.
seo-title: Añadir oyentes para notificaciones de metadatos temporizadas
title: Añadir oyentes para notificaciones de metadatos temporizadas
uuid: dcd1bd92-0617-4eab-8b06-7301aaff42f3
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Añadir oyentes para notificaciones de metadatos temporizadas {#add-listeners-for-timed-metadata-notifications}

Para recibir notificaciones sobre etiquetas en el manifiesto, implemente los oyentes de notificación correspondientes.

Puede supervisar los metadatos temporizados escuchando los siguientes eventos, que notifican a la aplicación la actividad relacionada:

* `PTTimedMetadataChangedNotification`:: Cada vez que se identifica una etiqueta suscrita única durante el análisis del contenido, TVSDK prepara un nuevo  `PTTimedMetadata` objeto y distribuye esta notificación.

   El objeto contiene el nombre de la etiqueta a la que se suscribió, la hora local de la reproducción en la que aparecerá esta etiqueta y otros datos.

* `PTMediaPlayerTimeChangeNotification` :: En el caso de flujos en directo/lineales en los que el manifiesto/lista de reproducción se actualiza periódicamente, es posible que aparezcan etiquetas personalizadas adicionales en la lista de reproducción/manifiesto actualizado, por lo que se pueden añadir  `TimedMetadata` objetos adicionales a la  `MediaPlayerItem.timedMetadata` propiedad.

   Este evento notifica a la aplicación cuando esto sucede.

   Recupere los metadatos temporizados de una de las siguientes formas.

   * Configure la aplicación para que se agregue como oyente a la notificación `PTTimedMetadataChangedNotification` y busque el objeto mediante `PTTimedMetadataKey`.

      ```
      [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onTimedMetadataChanged:)  
        name:PTTimedMetadataChangedNotification object:self.player.currentItem]; 
      
      - (void) onTimedMetadataChanged:(NSNotification *) notification { 
          NSDictionary *timedMetadataUserInfo = [[NSDictionary alloc]initWithDictionary: notification.userInfo]; 
          PTTimedMetadata *newTimedMetadata = [timedMetadataUserInfo objectForKey: PTTimedMetadataKey]; 
      }
      ```

   * Acceda a la propiedad `timedMetadataCollection` de `PTMediaPlayerItem`, que consta de todos los objetos `PTTimedMetadata` notificados hasta ahora.

