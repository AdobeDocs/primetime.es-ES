---
description: Los objetos PTNotification proporcionan información sobre cambios en el estado del reproductor, advertencias y errores. Los errores que detienen la reproducción del vídeo también provocan un cambio en el estado del reproductor.
title: Notificaciones de estado del reproductor, actividad, errores y registros
exl-id: 7f622c42-bc39-46e9-9b8b-4b3e467f37f7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# Notificaciones de estado del reproductor, actividad, errores y registro  {#notifications-for-player-status-activity-errors-and-logs-overview}

Los objetos PTNotification proporcionan información sobre cambios en el estado del reproductor, advertencias y errores. Los errores que detienen la reproducción del vídeo también provocan un cambio en el estado del reproductor.

La aplicación puede recuperar la información de notificación y estado. También puede crear un sistema de registro para diagnósticos y validación utilizando la información de notificación.

>[!IMPORTANT]
>
>TVSDK también utiliza *`notification`* para consultar `NSNotifications` ( `PTMediaPlayer` notifications) *`event`* notificaciones, enviadas para proporcionar información sobre la actividad del reproductor.

TVSDK también presenta problemas `PTMediaPlayerNewNotificationItemEntryNotification` cuando se emita `PTNotification`.

Los oyentes de eventos se implementan para capturar eventos y responder a ellos. Muchos eventos proporcionan `PTNotification` notificaciones de estado.

## Contenido de notificación {#notification-content}

PTNotification proporciona información relacionada con el estado del reproductor.

TVSDK proporciona una lista cronológica de `PTNotification` notificaciones. Cada notificación contiene la siguiente información:

* Marca de tiempo
* Metadatos de diagnóstico que constan de los siguientes elementos:

   * `type`: INFO, WARN o ERROR.
   * `code`: una representación numérica de la notificación.
   * `name`: una descripción legible en lenguaje natural de la notificación, como SEEK_ERROR
   * `metadata`: Pares de clave/valor que contienen información relevante sobre la notificación. Por ejemplo, una clave denominada `URL` proporciona un valor que es una dirección URL relacionada con la notificación.

   * `innerNotification`: una referencia a otra `PTNotification` que afecta directamente a esta notificación.

Puede almacenar esta información localmente para su posterior análisis o enviarla a un servidor remoto para su registro y representación gráfica.

## Configuración de notificaciones {#notification-setup}

TVSDK configura el reproductor para las notificaciones básicas, aunque debe completar la misma configuración para las notificaciones personalizadas.

Hay dos implementaciones para `PTNotification`:

* Para escuchar
* Para agregar notificaciones personalizadas a `PTNotificationHistory`

Para escuchar notificaciones, TVSDK crea una instancia de `PTNotification` y lo adjunta a una instancia de la clase `PTMediaPlayerItem`, que se adjunta a una instancia de PTMediaPlayer. Solo hay uno `PTNotificationHistory` instancia por `PTMediaPlayer`.

>[!IMPORTANT]
>
>Si va a agregar personalizaciones, las aplicaciones, y no TVSDK, deben realizar estos pasos.

## Escuchar notificaciones {#listen-to-notifications}

Hay dos maneras de escuchar el `PTNotification` notificación en el `PTMediaPlayer`:

1. Compruebe manualmente la `PTNotificationHistory` de la `PTMediaPlayerItem` con un temporizador y compruebe las diferencias:

   ```
   //Access to the PTMediaPlayerItem  
   PTMediaPlayerItem *item = self.player.currentItem; 
   PTNotificationHistory *notificationHistory = item.notificationHistory; 
   
   //Get the list of notification events from the notification History  
   NSArray *notifications = notificationHistory.notificationItems;
   ```

1. Usar el publicado [NSNotification](https://developer.apple.com/library/mac/%23documentation/Cocoa/Reference/Foundation/Classes/NSNotification_Class/Reference/Reference.html) de la `PTMediaPlayerPTMediaPlayerNewNotificationEntryAddedNotification`.
1. Regístrese en `NSNotification` mediante la instancia de `PTMediaPlayer` del que desea obtener notificaciones:

   ```
   //Register to the NSNotification 
   
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerNotification:)  
     name:PTMediaPlayerNewNotificationEntryAddedNotification object:self.player];
   ```

## Implementación de llamadas de retorno {#implement-notification-callbacks}

Puede implementar devoluciones de llamadas de notificación.

1. Implemente la llamada de retorno de la notificación obteniendo `PTNotification` desde el `NSNotification` información del usuario y lectura de sus valores mediante `PTMediaPlayerNotificationKey`:

   ```
   - (void) onMediaPlayerNotification:(NSNotification *) nsnotification { 
       PTNotification *notification = [nsnotification.userInfo objectForKey:PTMediaPlayerNotificationKey]; 
       NSLog(@"Notification: %@", notification); 
   }
   ```

## Añadir notificaciones personalizadas {#add-custom-notifications}

Para añadir una notificación personalizada: Crear una nueva `PTNotification` y agréguelo a la `PTNotificationHistory` mediante el uso del `PTMediaPlayerItem`:

```
//Access to the PTMediaPlayerItem  
PTMediaPlayerItem *item = self.player.currentItem; 
PTNotificationHistory *notificationHistory = item.notificationHistory; 
 
//Create notification 
PTNotification* notification = [[PTNotification notificationWithType:PTNotificationTypeWarning code:99999 description:@"Custom notification description"]; 
 
//Add notification 
[notificationHistory addNotification:notification];
```
