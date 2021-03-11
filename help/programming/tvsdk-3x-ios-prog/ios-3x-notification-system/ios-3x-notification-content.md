---
description: Los objetos PTNotification proporcionan información sobre cambios en el estado del reproductor, advertencias y errores. Los errores que detienen la reproducción del vídeo también provocan un cambio en el estado del reproductor.
title: Contenido de la notificación
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---


# Notificaciones del estado, la actividad, los errores y el registro del reproductor {#notifications-player-status-activity-errors-logging}

`PTNotification` Los objetos proporcionan información sobre cambios en el estado del reproductor, advertencias y errores. Los errores que detienen la reproducción del vídeo también provocan un cambio en el estado del reproductor.

La aplicación puede recuperar la información de notificación y estado. También puede crear un sistema de registro para diagnósticos y validación mediante la información de notificación.

>[!NOTE]
>
>TVSDK también utiliza *`notification`* para hacer referencia a las `NSNotifications` ( `PTMediaPlayer` notificaciones) *`event`* notificaciones, enviadas para proporcionar información sobre la actividad del reproductor.

TVSDK también emite `PTMediaPlayerNewNotificationItemEntryNotification` cuando emite `PTNotification`.

Los oyentes de eventos se implementan para capturar y responder a eventos. Muchos eventos proporcionan notificaciones de estado `PTNotification`.

## Contenido de notificación {#notification-content}

`PTNotification` proporciona información relacionada con el estado del reproductor.

TVSDK proporciona una lista cronológica de notificaciones `PTNotification`. Cada notificación contiene la siguiente información:

* Marca de tiempo
* Metadatos de diagnóstico que constan de los siguientes elementos:

   * `type`: INFO, WARN o ERROR.
   * `code`: Una representación numérica de la notificación.
   * `name`: Una descripción de la notificación legible en lenguaje natural, como SEEK_ERROR
   * `metadata`: Pares clave/valor que contienen información relevante sobre la notificación. Por ejemplo, una clave denominada `URL` proporciona un valor que es una dirección URL relacionada con la notificación.

   * `innerNotification`: Referencia a otro  `PTNotification` objeto que afecta directamente a esta notificación.

Puede almacenar esta información localmente para análisis posteriores o enviarla a un servidor remoto para el registro y la representación gráfica.

## Configuración de notificaciones {#notification-setup}

TVSDK configura el reproductor para las notificaciones básicas, aunque debe completar la misma configuración para las notificaciones personalizadas.

Existen dos implementaciones para `PTNotification`:

* Para escuchar
* Para agregar notificaciones personalizadas a `PTNotificationHistory`

Para escuchar las notificaciones, TVSDK crea una instancia de la clase `PTNotification` y la adjunta a una instancia de `PTMediaPlayerItem`, que se adjunta a una instancia de PTMediaPlayer. Solo hay una instancia `PTNotificationHistory` por `PTMediaPlayer`.

>[!IMPORTANT]
>
>Si agrega personalizaciones, las aplicaciones y no el TVSDK deben realizar estos pasos.

## Escuchar notificaciones {#listen-to-notifications}

Existen dos maneras de escuchar la notificación `PTNotification` en el `PTMediaPlayer`:

1. Compruebe manualmente el `PTNotificationHistory` del `PTMediaPlayerItem` con un temporizador y compruebe las diferencias:

   ```
   //Access to the PTMediaPlayerItem  
   PTMediaPlayerItem *item = self.player.currentItem; 
   PTNotificationHistory *notificationHistory = item.notificationHistory; 
   
   //Get the list of notification events from the notification History  
   NSArray *notifications = notificationHistory.notificationItems;
   ```

1. Utilice la [NSNotification](https://developer.apple.com/library/mac/%23documentation/Cocoa/Reference/Foundation/Classes/NSNotification_Class/Reference/Reference.html) publicada del `PTMediaPlayerPTMediaPlayerNewNotificationEntryAddedNotification`.
1. Regístrese en `NSNotification` utilizando la instancia de `PTMediaPlayer` desde la que desea obtener notificaciones:

   ```
   //Register to the NSNotification 
   
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerNotification:)  
     name:PTMediaPlayerNewNotificationEntryAddedNotification object:self.player];
   ```

## Implementar llamadas de retorno de notificación {#implement-notification-callbacks}

Puede implementar llamadas de retorno de notificación.

Implemente la llamada de retorno de notificación obteniendo el `PTNotification` de la información del usuario `NSNotification` y leyendo sus valores utilizando `PTMediaPlayerNotificationKey`:

```
- (void) onMediaPlayerNotification:(NSNotification *) nsnotification { 
    PTNotification *notification = [nsnotification.userInfo objectForKey:PTMediaPlayerNotificationKey]; 
    NSLog(@"Notification: %@", notification); 
}
```

## Añadir notificaciones personalizadas {#add-custom-notifications}

Para añadir una notificación personalizada:
Cree un nuevo `PTNotification` y agréguelo al `PTNotificationHistory` utilizando el `PTMediaPlayerItem` actual:

```
//Access to the PTMediaPlayerItem  
PTMediaPlayerItem *item = self.player.currentItem; 
PTNotificationHistory *notificationHistory = item.notificationHistory; 
 
//Create notification 
PTNotification* notification = [[PTNotification notificationWithType:PTNotificationTypeWarning code:99999 description:@"Custom notification description"]; 
 
//Add notification 
[notificationHistory addNotification:notification];
```
