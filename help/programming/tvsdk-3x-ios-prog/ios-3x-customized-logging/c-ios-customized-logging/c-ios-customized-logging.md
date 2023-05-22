---
description: Puede implementar su propio sistema de registro.
title: Explicación del registro personalizado
exl-id: 8b6a916e-783e-40e1-8a3d-706b57a6ff63
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# Registro personalizado {#customized-logging}

Puede implementar su propio sistema de registro.

Además de registrar mediante notificaciones predefinidas, puede implementar un sistema de registro que utilice sus mensajes de registro y los mensajes generados por TVSDK. Para obtener más información sobre las notificaciones predefinidas, consulte [El sistema de notificación](https://help.adobe.com/en_US/primetime/psdk/ios/index.html#PSDKs-concept-The_Notification_System). Puede utilizar estos registros para solucionar los problemas de las aplicaciones de reproducción y proporcionar una mejor comprensión del flujo de trabajo de reproducción y publicidad.

El registro personalizado utiliza una instancia singleton compartida del `PSDKPTLogFactory`, que proporciona un mecanismo para registrar mensajes en varios registradores. Puede definir y agregar (registrar) uno o más registradores al `PTLogFactory`. Esto le permite definir varios registradores con implementaciones personalizadas, como un registrador de consola, un registrador web o un registrador del historial de la consola.

TVSDK genera mensajes de registro para muchas de sus actividades, que el `PTLogFactory` reenvía a todos los registradores registrados. Su aplicación también puede generar mensajes de registro personalizados, que se reenvían a todos los registradores registrados. Cada registrador puede filtrar los mensajes y realizar las acciones adecuadas.

Hay dos implementaciones para `PTLogFactory`:

* Para escuchar registros.
* Para agregar registros a `PTLogFactory`.

## Escuchar registros {#listen-to-logs}

Para registrarse y escuchar registros:
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

1. Para registrar la instancia para recibir entradas de registro, agregue una instancia de `PTLogger` a la `PTLoggerFactory`:

   ```
   PTConsoleLogger *logger = [PTConsoleLogger consoleLogger]; 
   // Either use the addLogger method: 
   [[PTLogFactory sharedInstance] addLogger:(logger)] 
   
   //Or replace the preceding line with this macro for ease of use 
   //PTLogAddLogger(logger); 
   ```

<!--<a id="example_3738B5A8B4C048D28695E62297CF39E3"></a>-->

A continuación, se muestra un ejemplo de filtrado de registros utilizando `PTLogEntry` tipo:

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

Crear un nuevo `PTLogEntry` y añadirlo a `thePTLogFactory`:

Puede crear manualmente una instancia de `PTLogEntry` y agréguelo a la `PTLogFactory` instancia compartida o utilice una de las macros para realizar la misma tarea.

Este es un ejemplo de registro con `PTLogDebug` macro:

<!--<a id="example_F014436E1686468F941F4EBD1A21B18E"></a>-->

```
// The following line creates an instance of PTLogEntry with type PTLogEntryDebug, 
// tag "DEBUG_PLAYBACK", and message "Playback has started". 
// Then the PTLogEntry is automatically added to the PTLogFactory  
 
PTLogDebug(@"[DEBUG_PLAYBACK] Playback has started");
```
