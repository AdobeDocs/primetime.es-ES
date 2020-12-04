---
description: Puede implementar su propio sistema de registro.
seo-description: Puede implementar su propio sistema de registro.
seo-title: Registro personalizado
title: Registro personalizado
uuid: c5bdf266-4266-4896-b6e0-47710ce64e67
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---


# Registro personalizado {#customized-logging}

Puede implementar su propio sistema de registro.

Además de registrar mediante notificaciones predefinidas, puede implementar un sistema de registro que utilice los mensajes de registro y los mensajes generados por TVSDK. Para obtener más información sobre las notificaciones predefinidas, consulte [Sistema de notificaciones](../c-psdk-ios-1.4-notification-system/c-psdk-ios-1.4-notification-system.md). Puede utilizar estos registros para solucionar los problemas de las aplicaciones del reproductor y para comprender mejor el flujo de trabajo de la reproducción y la publicidad.

El registro personalizado utiliza una instancia singleton compartida de `PSDKPTLogFactory`, que proporciona un mecanismo para registrar mensajes en varios registradores. Puede definir y agregar (registrar) uno o más registros a `PTLogFactory`. Esto le permite definir varios registradores con implementaciones personalizadas, como un registrador de consola, un registrador web o un registrador de historial de consola.

TVSDK genera mensajes de registro para muchas de sus actividades, que el `PTLogFactory` reenvía a todos los registradores registrados. La aplicación también puede generar mensajes de registro personalizados, que se reenvían a todos los registradores registrados. Cada registrador puede filtrar los mensajes y tomar las medidas apropiadas.

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

1. Para registrar la instancia para recibir entradas de registro, agregue una instancia de `PTLogger` a `PTLoggerFactory`:

   ```
   PTConsoleLogger *logger = [PTConsoleLogger consoleLogger]; 
   // Either use the addLogger method: 
   [[PTLogFactory sharedInstance] addLogger:(logger)] 
   
   //Or replace the preceding line with this macro for ease of use 
   //PTLogAddLogger(logger); 
   ```

<!--<a id="example_3738B5A8B4C048D28695E62297CF39E3"></a>-->

A continuación se muestra un ejemplo de filtrado de registros utilizando el tipo `PTLogEntry`:

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

## Añadir nuevos mensajes de registro {#add-new-log-messages}

Para registrarse y escuchar los registros:
1. Cree un nuevo `PTLogEntry` y agréguelo a `thePTLogFactory`:

   Puede crear manualmente una instancia `PTLogEntry` y agregarla a la instancia `PTLogFactory` compartida o utilizar una de las macros para realizar la misma tarea.

   A continuación se muestra un ejemplo de registro con la macro `PTLogDebug`:

<!--<a id="example_F014436E1686468F941F4EBD1A21B18E"></a>-->

```
// The following line creates an instance of PTLogEntry with type PTLogEntryDebug, 
// tag "DEBUG_PLAYBACK", and message "Playback has started". 
// Then the PTLogEntry is automatically added to the PTLogFactory  
 
PTLogDebug(@"[DEBUG_PLAYBACK] Playback has started");
```
