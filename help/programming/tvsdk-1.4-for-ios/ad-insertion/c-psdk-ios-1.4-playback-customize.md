---
description: Cuando la reproducción llega a una pausa publicitaria, pasa una pausa publicitaria o termina en una pausa publicitaria, TVSDK define un comportamiento predeterminado para la posición del cursor de reproducción actual.
seo-description: Cuando la reproducción llega a una pausa publicitaria, pasa una pausa publicitaria o termina en una pausa publicitaria, TVSDK define un comportamiento predeterminado para la posición del cursor de reproducción actual.
seo-title: Personalización de la reproducción con anuncios
title: Personalización de la reproducción con anuncios
uuid: 58002ec2-65ab-4e3b-8e3b-f755ced5cb5a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 0%

---


# Personalizar la reproducción con anuncios{#customize-playback-with-ads}

Cuando la reproducción llega a una pausa publicitaria, pasa una pausa publicitaria o termina en una pausa publicitaria, TVSDK define un comportamiento predeterminado para la posición del cursor de reproducción actual.

>[!TIP]
>
>Puede anular el comportamiento predeterminado mediante la clase `PTAdPolicySelector`.

El comportamiento predeterminado varía en función de si el usuario pasa la pausa publicitaria durante la reproducción normal o de si busca en un vídeo.

Puede personalizar el comportamiento de la reproducción de publicidad de las siguientes formas:

* Guarde la posición en la que el usuario dejó de ver el vídeo y reanuda la reproducción en la misma posición en una sesión futura.
* Si se presenta una pausa publicitaria al usuario, no se muestran anuncios adicionales durante un número de minutos, aunque el usuario busque una nueva posición.
* Si el contenido no se reproduce después de unos minutos, reinicie el flujo o vuelva a una fuente diferente para el mismo contenido.

   En la sesión de reproducción de conmutación por error, para permitir que el usuario omita los anuncios y vuelva a la posición de error anterior, puede desactivar los anuncios anteriores y/o medios. TVSDK proporciona métodos para permitir omitir anuncios anteriores y finales.

## Elementos de API para reproducción de publicidad {#section_296ADE00CFEA40CBA1B46142720D13A5}

TVSDK proporciona clases y métodos que puede utilizar para personalizar el comportamiento de reproducción del contenido que contiene publicidad.
Los siguientes elementos de API son útiles para personalizar la reproducción:

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Elemento API </th> 
   <th colname="col2" class="entry"> Contenido que admite publicidad </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdMetadata  </span> </td> 
   <td colname="col2"> Controle si un salto de publicidad debe marcarse como visto por un visor y, en caso afirmativo, cuándo debe marcarse. Establezca y obtenga la directiva observada mediante la propiedad <span class="codeph"> adBreakAsWatched </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdPolicySelector  </span> </td> 
   <td colname="col2"> Protocolo que permite personalizar el comportamiento de la publicidad TVSDK. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTDefaultAdPolicySelector  </span> </td> 
   <td colname="col2"> Clase que implementa el comportamiento predeterminado de TVSDK. La aplicación puede anular esta clase para personalizar los comportamientos predeterminados sin implementar la interfaz completa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTMediaPlayer  </span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"> <span class="codeph"> localTime  </span>. <p>Es la hora local de la reproducción, excluyendo las pausas publicitarias colocadas. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"> <span class="codeph"> searchToLocalTime  </span> . <p>Aquí, la búsqueda se produce en relación con una hora local del flujo. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"> <span class="codeph"> getTimeline.convertToLocalTime  </span>. <p>La posición virtual en la línea de tiempo se convierte a la posición local. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdBreak  </span> </td> 
   <td colname="col2"> <span class="codeph"> isWatched,  </span> propiedad. Indica si el visor ha visto la publicidad. </td> 
  </tr> 
 </tbody> 
</table>

## Configurar la reproducción personalizada {#section_8209BAACC7814C9399988DC7DE9CF4CA}

Para poder personalizar o anular los comportamientos de publicidad, registre la instancia de directiva de publicidad con TVSDK.

Para personalizar los comportamientos de las publicidades, realice una de las siguientes acciones:

* Conformidad con el protocolo `PTAdPolicySelector` e implemente todos los métodos de selección de directivas necesarios.

   Esta opción se recomienda si necesita anular **todos** los comportamientos de publicidad predeterminados.

* Omitir la clase `PTDefaultAdPolicySelector` y proporcionar implementaciones solo para los comportamientos que requieren personalización.

   Esta opción se recomienda si necesita anular sólo **algunos** de los comportamientos predeterminados.

Para ambas opciones, complete las siguientes tareas:

1. Registre la instancia de directiva que usará TVSDK a través de la fábrica del cliente.

   >[!NOTE]
   >
   >Las directivas de publicidad personalizadas registradas al principio de la reproducción se borran cuando se desasigna la instancia `PTMediaPlayer`. La aplicación debe registrar una instancia de selector de políticas cada vez que se cree una nueva sesión de reproducción.

   Por ejemplo:

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. Implemente sus personalizaciones.

## Omitir pausas publicitarias para un período de tiempo {#section_99809BE4D9BB4DEEBBF596C746CA428A}

De forma predeterminada, TVSDK fuerza la reproducción de una pausa publicitaria cuando el usuario busca durante una pausa publicitaria. Puede personalizar el comportamiento para omitir una pausa publicitaria si el tiempo transcurrido desde la finalización de una pausa anterior es de un número determinado de minutos.

>[!IMPORTANT]
>
>Cuando hay una búsqueda interna para omitir una publicidad, puede que haya una ligera pausa en la reproducción.

El siguiente ejemplo de selector de directivas de publicidad personalizado omite las publicidades en los próximos cinco minutos (tiempo de reloj de pared) después de que un usuario haya visto una pausa publicitaria.

1. Registre la instancia de directiva que usará TVSDK a través de la fábrica del cliente.

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. Implemente su personalización.

**PTS5MinuteSkipBreakPolicySelector.h**

```
#import "PTMediaPlayerNotifications.h" 
#import "PTMediaPlayer.h" 
#import "PTDefaultAdPolicySelector.h" 
 
//  extend the default policy  
selector@interface PTS5MinuteSkipBreakPolicySelector : PTDefaultAdPolicySelector 
  
- (id)initWithMediaPlayer:(PTMediaPlayer *)player; 
  
@end
```

**PTS5MinuteSkipBreakPolicySelector.m**

```
#import "PTS5MinuteSkipBreakPolicySelector.h" 
  
double MIN_BREAK_INTERVAL  = 60 * 5; // 5 minutes 
  
@implementation PTS5MinuteSkipBreakPolicySelector 
{ 
    PTMediaPlayer *_player; 
    NSTimeInterval _lastAdBreakPlayedTime; 
} 
  
- (id)initWithMediaPlayer:(PTMediaPlayer *)player 
{ 
    if (self = [super init]) 
    { 
        _lastAdBreakPlayedTime = 0; 
        _player = [player retain]; 
        [self addobservers]; 
    } 
    
    return self; 
} 
  
- (NSArray *)selectAdBreaksToPlay:(PTAdPolicyInfo *)info 
{ 
    NSLog(@"%@ - selectAdBreaksToPlay (%f): %f", self,  
        CMTimeGetSeconds(info.currentTime), _lastAdBreakPlayedTime); 
    
    BOOL shouldPlay = [self shouldPlayAdBreaks]; 
    if (shouldPlay) 
    { 
        return [super selectAdBreaksToPlay:info]; 
    } 
    
    return nil; 
} 
  
- (PTAdBreakPolicyType)selectPolicyForAdBreak:(PTAdPolicyInfo *)info 
{ 
    NSLog(@"%@ - selectPolicyForAdBreak (%f): %f  %f", self,  
            CMTimeGetSeconds(info.currentTime), _lastAdBreakPlayedTime,  
            [[NSDate date] timeIntervalSince1970]); 
    
    BOOL shouldPlay = [self shouldPlayAdBreaks]; 
    if (shouldPlay) 
    { 
        return [super selectPolicyForAdBreak:info]; 
    } 
    
    return PTAdBreakPolicyTypeSkip; 
} 
  
- (BOOL)shouldPlayAdBreaks 
{ 
    NSTimeInterval currentTime = [[NSDate date] timeIntervalSince1970]; 
    if (_lastAdBreakPlayedTime <= 0) 
    { 
        return YES; 
    } 
    
    if (_lastAdBreakPlayedTime > 0 && (currentTime - _lastAdBreakPlayedTime) > MIN_BREAK_INTERVAL) 
    { 
        return YES; 
    } 
    
    // don't play any ad break if 5 minutes hasn't elapsed 
    return NO; 
} 
  
- (void) onMediaPlayerAdBreakStarted:(NSNotification *) notification 
{ 
    NSLog(@"%@ - AdBreak Start", self); 
} 
  
- (void) onMediaPlayerAdBreakCompleted:(NSNotification *) notification 
{ 
    _lastAdBreakPlayedTime = [[NSDate date] timeIntervalSince1970]; 
    NSLog(@"%@ - AdBreak Complete at: %f", self, _lastAdBreakPlayedTime); 
} 
  
- (void)addobservers 
{ 
    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdBreakStarted:)  
                name:PTMediaPlayerAdBreakStartedNotification object:_player]; 
    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdBreakCompleted:)  
                name:PTMediaPlayerAdBreakCompletedNotification object:_player]; 
} 
  
- (void)removeObservers 
{ 
    [[NSNotificationCenter defaultCenter] removeObserver:self]; 
} 
  
- (void)dealloc 
{ 
    [self removeObservers]; 
    [_player release]; 
    [super dealloc]; 
} 
  
@end
```

## Guarde la posición del vídeo y reanude más tarde {#section_FAE252E38CED48D4BDD38BAA4A6A20A4}

Puede guardar la posición de reproducción actual en un vídeo y reanudar la reproducción en la misma posición en una sesión futura.

Las publicidades insertadas dinámicamente difieren entre las sesiones de usuario, por lo que al guardar la posición **con** publicidades duplicadas se hace referencia a una posición diferente en una sesión futura. TVSDK proporciona métodos para recuperar la posición de reproducción e ignorar las publicidades duplicadas.

1. Cuando el usuario cierra un vídeo, la aplicación recupera y guarda la posición en el vídeo.

   >[!TIP]
   >
   >No se incluyen las duraciones de los anuncios.

   Los saltos de publicidad pueden variar en cada sesión debido a patrones de publicidad, límites de frecuencia, etc. La hora actual del vídeo en una sesión puede ser diferente en una sesión futura. Al guardar una posición en el vídeo, la aplicación recupera la hora local. Utilice la propiedad `localTime` para leer esta posición, que puede guardar en el dispositivo o en una base de datos del servidor.

   Por ejemplo: si el usuario se encuentra en el minuto 20 del video y esta posición incluye cinco minutos de anuncios, `currentTime` será de 1200 segundos, mientras que `localTime` en esta posición será de 900 segundos.

   >[!IMPORTANT]
   >
   >La hora local y la hora actual son las mismas para flujos en directo/lineales. En este caso, `convertToLocalTime` no tiene ningún efecto. Para VOD, el tiempo local permanece sin cambios mientras se reproducen los anuncios.

   ```
   - (void) onMediaPlayerTimeChange:(NSNotification *)notification { 
       CMTimeRange seekableRange = self.player.seekableRange; 
   
       if (CMTIMERANGE_IS_VALID(seekableRange)) { 
           double seekableRangeStart = CMTimeGetSeconds(seekableRange.start); 
           double seekableRangeDuration = CMTimeGetSeconds(seekableRange.duration); 
           double currentTime = CMTimeGetSeconds(self.player.currentTime); // includes ads 
           double localTime = CMTimeGetSeconds(self.player.localTime); // no ads 
       } 
   }
   ```

1. Para reanudar el vídeo en la misma posición: Para reanudar la reproducción del vídeo desde la posición guardada en una sesión anterior, utilice `seekToLocalTime`

   >[!TIP]
   >
   >Este método solo se llama con valores de hora locales. Si se llama al método con los resultados de tiempo actuales, se produce un comportamiento incorrecto.

   Para buscar la hora actual, utilice `seekToTime`.

1. Cuando la aplicación reciba el evento de cambio de estado `PTMediaPlayerStatusReady`, busque la hora local guardada.

   ```
   [self.player seekToLocalTime:CMTimeMake(900, 1) completionHandler:^(BOOL finished) { 
       [self.player play]; 
   }];
   ```

1. Proporcione los saltos de publicidad como se especifica en la interfaz de directivas de publicidad.
1. Implemente un selector de directivas de publicidad personalizado ampliando el selector de directivas de publicidad predeterminado.
1. Proporcione los saltos de publicidad que deben presentarse al usuario implementando `selectAdBreaksToPlay`

   >[!NOTE]
   >
   >Este método incluye una pausa publicitaria previa y las pausas publicitarias intermedias antes de la posición horaria local. La aplicación puede decidir reproducir una pausa publicitaria previa y reanudar a la hora local especificada, reproducir una pausa publicitaria media y reanudar a la hora local especificada o no reproducir ninguna pausa publicitaria.

