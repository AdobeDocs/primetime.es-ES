---
description: Puede implementar su propio sistema de registro.
title: Registro personalizado
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---


# Registro personalizado {#customized-logging}

Puede implementar su propio sistema de registro.

Además de iniciar sesión mediante notificaciones predefinidas, puede implementar un sistema de registro que utilice los mensajes de registro y los mensajes generados por TVSDK. Para obtener más información sobre las notificaciones predefinidas, consulte [El sistema de notificaciones](../c-psdk-ios-1.4-notification-system/c-psdk-ios-1.4-notification-system.md). Puede utilizar estos registros para solucionar problemas en las aplicaciones del reproductor y para comprender mejor el flujo de trabajo de reproducción y publicidad.

El registro personalizado utiliza una instancia singleton compartida de `PSDKPTLogFactory`, que proporciona un mecanismo para registrar mensajes en varios registros. Puede definir y agregar (registrar) uno o más registros a `PTLogFactory`. Esto le permite definir varios registros con implementaciones personalizadas, como un registrador de consola, un registrador web o un registrador de historial de consola.

TVSDK genera mensajes de registro para muchas de sus actividades, que el `PTLogFactory` reenvía a todos los registros registrados. La aplicación también puede generar mensajes de registro personalizados, que se reenvían a todos los registros registrados. Cada registrador puede filtrar los mensajes y tomar las medidas adecuadas.

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

1. Para registrar la instancia para recibir entradas de registro, añada una instancia de `PTLogger` al `PTLoggerFactory`:

   ```
   PTConsoleLogger *logger = [PTConsoleLogger consoleLogger]; 
   // Either use the addLogger method: 
   [[PTLogFactory sharedInstance] addLogger:(logger)] 
   
   //Or replace the preceding line with this macro for ease of use 
   //PTLogAddLogger(logger); 
   ```

<!--<a id="example_3738B5A8B4C048D28695E62297CF39E3"></a>-->

Este es un ejemplo de filtrado de registros mediante el tipo `PTLogEntry` :

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

Para registrarse y escuchar registros:
1. Cree un nuevo `PTLogEntry` y agréguelo a `thePTLogFactory`:

   Puede crear una instancia `PTLogEntry` manualmente y agregarla a la instancia compartida `PTLogFactory` o utilizar una de las macros para realizar la misma tarea.

   Este es un ejemplo de registro con la macro `PTLogDebug` :

<!--<a id="example_F014436E1686468F941F4EBD1A21B18E"></a>-->

```
// The following line creates an instance of PTLogEntry with type PTLogEntryDebug, 
// tag "DEBUG_PLAYBACK", and message "Playback has started". 
// Then the PTLogEntry is automatically added to the PTLogFactory  
 
PTLogDebug(@"[DEBUG_PLAYBACK] Playback has started");
```
