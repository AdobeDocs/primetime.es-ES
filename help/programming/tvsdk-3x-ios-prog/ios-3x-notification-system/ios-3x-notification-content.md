---
description: Los objetos PTNotification proporcionan información sobre los cambios en el estado del reproductor, las advertencias y los errores. Los errores que detienen la reproducción del vídeo también provocan un cambio en el estado del reproductor.
seo-description: Los objetos PTNotification proporcionan información sobre los cambios en el estado del reproductor, las advertencias y los errores. Los errores que detienen la reproducción del vídeo también provocan un cambio en el estado del reproductor.
seo-title: Contenido de notificación
title: Contenido de notificación
uuid: d42d2e89-1bdd-4be0-8a69-821fec6bbc75
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---


# Notificaciones de estado, actividad, errores y registro del reproductor {#notifications-player-status-activity-errors-logging}

`PTNotification` los objetos proporcionan información sobre los cambios en el estado del reproductor, las advertencias y los errores. Los errores que detienen la reproducción del vídeo también provocan un cambio en el estado del reproductor.

La aplicación puede recuperar la notificación y la información de estado. También puede crear un sistema de registro para diagnósticos y validación mediante la información de notificación.

>[!NOTE]
>
>TVSDK también utiliza *`notification`* para hacer referencia a `NSNotifications` ( `PTMediaPlayer` notificaciones) *`event`*, enviadas para proporcionar información sobre la actividad del reproductor.

TVSDK también emite `PTMediaPlayerNewNotificationItemEntryNotification` cuando emite `PTNotification`.

Los oyentes de evento se implementan para capturar y responder a eventos. Muchos eventos proporcionan `PTNotification` notificaciones de estado.

## Contenido de notificación {#notification-content}

`PTNotification` proporciona información relacionada con el estado del reproductor.

TVSDK proporciona una lista cronológica de las `PTNotification` notificaciones. Cada notificación contiene la siguiente información:

* Marca de hora
* Metadatos de diagnóstico que constan de los siguientes elementos:

   * `type`:: INFORMACIÓN, ADVERTENCIA o ERROR.
   * `code`:: Una representación numérica de la notificación.
   * `name`:: Descripción legible en lenguaje natural de la notificación, como SEEK_ERROR
   * `metadata`:: Pares clave/valor que contienen información relevante sobre la notificación. Por ejemplo, una clave denominada `URL` proporciona un valor que es una dirección URL relacionada con la notificación.

   * `innerNotification`:: Referencia a otro  `PTNotification` objeto que afecta directamente a esta notificación.

Puede almacenar esta información localmente para su posterior análisis o enviarla a un servidor remoto para que la registre y la represente en forma gráfica.

## Configuración de notificaciones {#notification-setup}

TVSDK configura el reproductor para las notificaciones básicas, aunque debe completar la misma configuración para las notificaciones personalizadas.

Existen dos implementaciones para `PTNotification`:

* Para escuchar
* Para agregar notificaciones personalizadas a `PTNotificationHistory`

Para escuchar las notificaciones, TVSDK crea una instancia de la clase `PTNotification` y la adjunta a una instancia de `PTMediaPlayerItem`, que se adjunta a una instancia de PTMediaPlayer. Sólo hay una instancia `PTNotificationHistory` por `PTMediaPlayer`.

>[!IMPORTANT]
>
>Si va a agregar personalizaciones, las aplicaciones, y no el TVSDK, deben realizar estos pasos.

## Escuchar notificaciones {#listen-to-notifications}

Existen dos maneras de escuchar la notificación `PTNotification` en `PTMediaPlayer`:

1. Compruebe manualmente el `PTNotificationHistory` del `PTMediaPlayerItem` con un temporizador y compruebe las diferencias:

   ```
   //Access to the PTMediaPlayerItem  
   PTMediaPlayerItem *item = self.player.currentItem; 
   PTNotificationHistory *notificationHistory = item.notificationHistory; 
   
   //Get the list of notification events from the notification History  
   NSArray *notifications = notificationHistory.notificationItems;
   ```

1. Utilice la [notificación NSN](https://developer.apple.com/library/mac/%23documentation/Cocoa/Reference/Foundation/Classes/NSNotification_Class/Reference/Reference.html) publicada de la `PTMediaPlayerPTMediaPlayerNewNotificationEntryAddedNotification`.
1. Regístrese en `NSNotification` mediante la instancia de `PTMediaPlayer` desde la que desea obtener las notificaciones:

   ```
   //Register to the NSNotification 
   
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerNotification:)  
     name:PTMediaPlayerNewNotificationEntryAddedNotification object:self.player];
   ```

## Implementar llamadas de retorno de notificación {#implement-notification-callbacks}

Puede implementar llamadas de retorno de notificación.

Implemente la devolución de llamada de notificación obteniendo `PTNotification` de la información del usuario `NSNotification` y leyendo sus valores mediante `PTMediaPlayerNotificationKey`:

```
- (void) onMediaPlayerNotification:(NSNotification *) nsnotification { 
    PTNotification *notification = [nsnotification.userInfo objectForKey:PTMediaPlayerNotificationKey]; 
    NSLog(@"Notification: %@", notification); 
}
```

## Añadir notificaciones personalizadas {#add-custom-notifications}

Para agregar una notificación personalizada:
Cree un `PTNotification` nuevo y agréguelo a `PTNotificationHistory` mediante el `PTMediaPlayerItem` actual:

```
//Access to the PTMediaPlayerItem  
PTMediaPlayerItem *item = self.player.currentItem; 
PTNotificationHistory *notificationHistory = item.notificationHistory; 
 
//Create notification 
PTNotification* notification = [[PTNotification notificationWithType:PTNotificationTypeWarning code:99999 description:@"Custom notification description"]; 
 
//Add notification 
[notificationHistory addNotification:notification];
```
