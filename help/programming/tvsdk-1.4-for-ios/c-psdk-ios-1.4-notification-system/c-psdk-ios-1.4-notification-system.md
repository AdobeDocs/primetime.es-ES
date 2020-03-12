---
description: Los objetos PTNotification proporcionan información sobre los cambios en el estado del reproductor, las advertencias y los errores. Los errores que detienen la reproducción del vídeo también provocan un cambio en el estado del reproductor.
seo-description: Los objetos PTNotification proporcionan información sobre los cambios en el estado del reproductor, las advertencias y los errores. Los errores que detienen la reproducción del vídeo también provocan un cambio en el estado del reproductor.
seo-title: Notificaciones de estado, actividad, errores y registros del reproductor
title: Notificaciones de estado, actividad, errores y registros del reproductor
uuid: 59716a66-3736-4076-8011-8104bfe3a83a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Notificaciones de estado, actividad, errores y registro del reproductor {#notifications-for-player-status-activity-errors-and-logs-overview}

Los objetos PTNotification proporcionan información sobre los cambios en el estado del reproductor, las advertencias y los errores. Los errores que detienen la reproducción del vídeo también provocan un cambio en el estado del reproductor.

La aplicación puede recuperar la notificación y la información de estado. También puede crear un sistema de registro para diagnósticos y validación mediante la información de notificación.

>[!IMPORTANT]
>
>TVSDK también utiliza *`notification`* para referirse a las notificaciones `NSNotifications` ( `PTMediaPlayer` notificaciones) *`event`* , enviadas para proporcionar información sobre la actividad del reproductor.

TVSDK también se emite `PTMediaPlayerNewNotificationItemEntryNotification` cuando se emite `PTNotification`.

Los oyentes de eventos se implementan para capturar y responder a los eventos. Muchos eventos proporcionan notificaciones `PTNotification` de estado.

## Contenido de notificación {#notification-content}

PTNotification proporciona información relacionada con el estado del reproductor.

TVSDK proporciona una lista cronológica de `PTNotification` notificaciones. Cada notificación contiene la siguiente información:

* Marca de hora
* Metadatos de diagnóstico que constan de los siguientes elementos:

   * `type`:: INFORMACIÓN, ADVERTENCIA o ERROR.
   * `code`:: Una representación numérica de la notificación.
   * `name`:: Descripción legible en lenguaje natural de la notificación, como SEEK_ERROR
   * `metadata`:: Pares clave/valor que contienen información relevante sobre la notificación. Por ejemplo, una clave llamada `URL` proporciona un valor que es una dirección URL relacionada con la notificación.

   * `innerNotification`:: Referencia a otro `PTNotification` objeto que afecta directamente a esta notificación.

Puede almacenar esta información de forma local para analizarla posteriormente o enviarla a un servidor remoto para que registre y muestre una representación gráfica.

## Configuración de notificaciones {#notification-setup}

TVSDK configura el reproductor para las notificaciones básicas, aunque debe completar la misma configuración para las notificaciones personalizadas.

Existen dos implementaciones para `PTNotification`:

* Para escuchar
* Para agregar notificaciones personalizadas a `PTNotificationHistory`

Para escuchar las notificaciones, TVSDK crea una instancia de la `PTNotification` clase y la adjunta a una instancia de `PTMediaPlayerItem`, que se adjunta a una instancia de PTMediaPlayer. Solo hay una `PTNotificationHistory` instancia por `PTMediaPlayer`.

>[!IMPORTANT]
>
>Si va a agregar personalizaciones, las aplicaciones, y no el TVSDK, deben realizar estos pasos.

## Escuchar notificaciones {#listen-to-notifications}

Existen dos maneras de escuchar la `PTNotification` notificación en la `PTMediaPlayer`:

1. Compruebe manualmente el funcionamiento `PTNotificationHistory` del `PTMediaPlayerItem` temporizador y compruebe las diferencias:

   ```
   //Access to the PTMediaPlayerItem  
   PTMediaPlayerItem *item = self.player.currentItem; 
   PTNotificationHistory *notificationHistory = item.notificationHistory; 
   
   //Get the list of notification events from the notification History  
   NSArray *notifications = notificationHistory.notificationItems;
   ```

1. Utilice la [notificación NSN](https://developer.apple.com/library/mac/%23documentation/Cocoa/Reference/Foundation/Classes/NSNotification_Class/Reference/Reference.html) publicada del `PTMediaPlayerPTMediaPlayerNewNotificationEntryAddedNotification`.
1. Regístrese en el `NSNotification` mediante la instancia del `PTMediaPlayer` formulario desde el que desea obtener las notificaciones:

   ```
   //Register to the NSNotification 
   
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerNotification:)  
     name:PTMediaPlayerNewNotificationEntryAddedNotification object:self.player];
   ```

## Implementar rellamadas de notificación {#implement-notification-callbacks}

Puede implementar llamadas de retorno de notificación.

1. Implemente la devolución de llamada de notificación obteniendo la información `PTNotification` del `NSNotification` usuario y leyendo sus valores mediante `PTMediaPlayerNotificationKey`:

   ```
   - (void) onMediaPlayerNotification:(NSNotification *) nsnotification { 
       PTNotification *notification = [nsnotification.userInfo objectForKey:PTMediaPlayerNotificationKey]; 
       NSLog(@"Notification: %@", notification); 
   }
   ```

## Agregar notificaciones personalizadas {#add-custom-notifications}

Para agregar una notificación personalizada:
Cree un nuevo `PTNotification` y agréguelo a la `PTNotificationHistory` página mediante la opción `PTMediaPlayerItem`:

```
//Access to the PTMediaPlayerItem  
PTMediaPlayerItem *item = self.player.currentItem; 
PTNotificationHistory *notificationHistory = item.notificationHistory; 
 
//Create notification 
PTNotification* notification = [[PTNotification notificationWithType:PTNotificationTypeWarning code:99999 description:@"Custom notification description"]; 
 
//Add notification 
[notificationHistory addNotification:notification];
```
