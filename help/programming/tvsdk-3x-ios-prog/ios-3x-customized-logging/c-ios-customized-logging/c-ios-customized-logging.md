---
description: Puede implementar su propio sistema de registro.
seo-description: Puede implementar su propio sistema de registro.
seo-title: Explicación del registro personalizado
title: Explicación del registro personalizado
uuid: f056d7d7-ec3a-4cf1-997f-72a89bbc9447
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Registro personalizado {#customized-logging}

Puede implementar su propio sistema de registro.

Además de registrar mediante notificaciones predefinidas, puede implementar un sistema de registro que utilice los mensajes de registro y los mensajes generados por TVSDK. Para obtener más información sobre las notificaciones predefinidas, consulte [El sistema](https://help.adobe.com/en_US/primetime/psdk/ios/index.html#PSDKs-concept-The_Notification_System)de notificaciones. Puede utilizar estos registros para solucionar los problemas de las aplicaciones del reproductor y para comprender mejor el flujo de trabajo de la reproducción y la publicidad.

El registro personalizado utiliza una instancia singleton compartida del `PSDKPTLogFactory`, que proporciona un mecanismo para registrar mensajes en varios registradores. Puede definir y agregar (registrar) uno o más registros al `PTLogFactory`. Esto le permite definir varios registradores con implementaciones personalizadas, como un registrador de consola, un registrador web o un registrador de historial de consola.

TVSDK genera mensajes de registro para muchas de sus actividades, que `PTLogFactory` reenvía a todos los registradores registrados. La aplicación también puede generar mensajes de registro personalizados, que se reenvían a todos los registradores registrados. Cada registrador puede filtrar los mensajes y tomar las medidas apropiadas.

Existen dos implementaciones para `PTLogFactory`:

* Para escuchar registros.
* Para agregar registros a un `PTLogFactory`.

## Escuchar registros {#listen-to-logs}

Para registrarse para escuchar registros:
1. Implemente una clase personalizada que siga el protocolo `PTLogger`:

   ```
   @implementation PTConsoleLogger 
   
   + (PTConsoleLogger *) consoleLogger { 
       return [[[PTConsoleLogger alloc] init] autorelease]; 
   } 
   
   - (void)logEntry:(PTLogEntry *)entry { 
       //Log the message to the console using NSLog  
       NSLog(@"[%@] %@", entry.tag, entry.message); 
   } 
   
   @end
   ```

1. Para registrar la instancia para recibir entradas de registro, agregue una instancia del `PTLogger` al `PTLoggerFactory`:

   ```
   PTConsoleLogger *logger = [PTConsoleLogger consoleLogger]; 
   // Either use the addLogger method: 
   [[PTLogFactory sharedInstance] addLogger:(logger)] 
   
   //Or replace the preceding line with this macro for ease of use 
   //PTLogAddLogger(logger); 
   ```

<!--<a id="example_3738B5A8B4C048D28695E62297CF39E3"></a>-->

A continuación se muestra un ejemplo de filtrado de registros mediante el `PTLogEntry` tipo:

```
@implementation PTConsoleLogger 
 
+ (PTConsoleLogger *) consoleLogger { 
    return [[[PTConsoleLogger alloc] init] autorelease]; 
} 
 
- (id) init { 
    self = [super init]; 
 
    if (self) { 
        self.logLevel = PTLogEntryTypeInfo; 
    } 
 
    return self; 
} 
 
- (void)logEntry:(PTLogEntry *) entry { 
    //Filtering the entry by log level  
    if (entry.type < _logLevel) { 
        return; 
    } 
 
    //Log the message to the console using NSLog NSLog(@"[%@] %@", entry.tag, entry.message); 
} 
 
@end
```

## Agregar nuevos mensajes de registro {#add-new-log-messages}

Para registrarse y escuchar los registros:

Cree un nuevo `PTLogEntry` y agréguelo a `thePTLogFactory`:

Puede crear manualmente una instancia `PTLogEntry` y agregarla a la instancia `PTLogFactory` compartida o utilizar una de las macros para realizar la misma tarea.

A continuación se muestra un ejemplo del registro mediante la `PTLogDebug` macro:

<!--<a id="example_F014436E1686468F941F4EBD1A21B18E"></a>-->

```
// The following line creates an instance of PTLogEntry with type PTLogEntryDebug, 
// tag "DEBUG_PLAYBACK", and message "Playback has started". 
// Then the PTLogEntry is automatically added to the PTLogFactory  
 
PTLogDebug(@"[DEBUG_PLAYBACK] Playback has started");
```
