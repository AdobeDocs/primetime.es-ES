---
description: Cuando la reproducción llega a una pausa publicitaria, pasa una pausa publicitaria o termina en una pausa publicitaria, TVSDK define algún comportamiento predeterminado para la colocación del cabezal de reproducción actual.
title: Personalización de la reproducción con anuncios
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 0%

---

# Personalización de la reproducción con anuncios {#customize-playback-with-ads}

Cuando la reproducción llega a una pausa publicitaria, pasa una pausa publicitaria o termina en una pausa publicitaria, TVSDK define algún comportamiento predeterminado para la colocación del cabezal de reproducción actual.

>[!TIP]
>
>Puede anular el comportamiento predeterminado utilizando la variable `PTAdPolicySelector` clase.

El comportamiento predeterminado varía en función de si el usuario pasa la pausa publicitaria durante la reproducción normal o buscando en un vídeo.

Puede personalizar el comportamiento de reproducción de la publicidad de las siguientes maneras:

* Guarde la posición en la que el usuario dejó de ver el vídeo y reanude la reproducción en la misma posición en una sesión futura.
* Si se presenta una pausa publicitaria al usuario, este no mostrará anuncios adicionales durante una serie de minutos, aunque busque una nueva posición.
* Si el contenido no se reproduce después de unos minutos, reinicie el flujo o realice una conmutación por error a un origen diferente para el mismo contenido.

  En la sesión de reproducción por error, para permitir que el usuario omita los anuncios y se reanude a la posición con error anterior, puede desactivar los anuncios previos a la emisión o los anuncios durante la emisión. TVSDK proporciona métodos para habilitar la omisión de anuncios previos a la emisión y anuncios durante la emisión.

## Elementos de API para la reproducción de publicidad {#section_296ADE00CFEA40CBA1B46142720D13A5}

TVSDK proporciona clases y métodos que puede utilizar para personalizar el comportamiento de reproducción del contenido que contiene publicidad.
Los siguientes elementos de la API son útiles para personalizar la reproducción:

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>Elemento API</b></th> 
   <th colname="col2" class="entry"><b>Contenido que admite publicidad</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdMetadata </span> </td> 
   <td colname="col2"> Controle si una pausa publicitaria debe marcarse como si hubiera sido visualizada por un visor y, en caso afirmativo, cuándo marcarla. Configurar y obtener la directiva vigilada mediante <span class="codeph"> adBreakAsWatched </span> propiedad. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdPolicySelector </span> </td> 
   <td colname="col2"> Protocolo que permite personalizar el comportamiento de anuncios de TVSDK. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTDefaultAdPolicySelector </span> </td> 
   <td colname="col2"> Clase que implementa el comportamiento predeterminado de TVSDK. La aplicación puede invalidar esta clase para personalizar los comportamientos predeterminados sin implementar la interfaz completa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTMediaPlayer </span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"> <span class="codeph"> localTime </span>. <p>Es la hora local de la reproducción, excluidas las pausas publicitarias colocadas. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"> <span class="codeph"> seekToLocalTime </span> . <p>En este caso, la búsqueda se produce en relación con una hora local de la secuencia. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"> <span class="codeph"> getTimeline.convertToLocalTime </span>. <p>La posición virtual en la cronología se convierte a la posición local. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PTAdBreak </span> </td> 
   <td colname="col2"> <span class="codeph"> isWatched </span> propiedad. Indica si el visualizador ha visto el anuncio. </td> 
  </tr> 
 </tbody> 
</table>

## Configuración de la reproducción personalizada {#section_8209BAACC7814C9399988DC7DE9CF4CA}

Para poder personalizar o anular los comportamientos de anuncio, registre la instancia de directiva de publicidad con TVSDK.

Para personalizar los comportamientos de los anuncios, realice una de las siguientes acciones:

* Conformidad con el `PTAdPolicySelector` e implementar todos los métodos de selección de directivas necesarios.

  Esta opción se recomienda si necesita anular la **todo** los comportamientos de anuncio predeterminados.

* Anular la variable `PTDefaultAdPolicySelector` y proporcionan implementaciones solo para los comportamientos que requieren personalización.

  Esta opción se recomienda si solo necesita anular la selección **algunos** de los comportamientos predeterminados.

Para ambas opciones, complete las siguientes tareas:

1. Registre la instancia de directiva que utilizará TVSDK a través de la fábrica del cliente.

   >[!NOTE]
   >
   >Las políticas de publicidad personalizadas que se registran al principio de la reproducción se borran cuando `PTMediaPlayer` La instancia de está desasignada. La aplicación debe registrar una instancia de selector de directivas cada vez que se cree una nueva sesión de reproducción.

   Por ejemplo:

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. Implementar las personalizaciones.

## Omitir pausas publicitarias durante un periodo de tiempo {#section_99809BE4D9BB4DEEBBF596C746CA428A}

De forma predeterminada, TVSDK fuerza la reproducción de una pausa publicitaria cuando el usuario realiza una búsqueda sobre una pausa publicitaria. Puede personalizar el comportamiento para omitir una pausa publicitaria si el tiempo transcurrido desde que se completó una pausa anterior se encuentra dentro de un determinado número de minutos.

>[!IMPORTANT]
>
>Cuando hay una búsqueda interna para omitir un anuncio, puede haber una ligera pausa en la reproducción.

El siguiente ejemplo de selector de políticas de publicidad personalizado omite los anuncios en los siguientes cinco minutos (hora del reloj mural) después de que un usuario haya visto una pausa publicitaria.

1. Registre la instancia de directiva que utilizará TVSDK a través de la fábrica del cliente.

   ```
   // Create an instance of the custom policy selector 
   PTS5MinuteSkipBreakPolicySelector *adPolicySelector  
        = [[[PTS5MinuteSkipBreakPolicySelector alloc] initWithMediaPlayer:self.player] autorelease]; 
   
   // register this instance 
   [[PTDefaultMediaPlayerClientFactory defaultFactory] registerAdPolicySelector:adPolicySelector];
   ```

1. Implemente la personalización.

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

## Guardar la posición del vídeo y reanudarlo más tarde {#section_FAE252E38CED48D4BDD38BAA4A6A20A4}

Puede guardar la posición de reproducción actual en un vídeo y reanudar la reproducción en la misma posición en una sesión futura.

Los anuncios insertados dinámicamente difieren entre las sesiones de usuario, por lo que se guarda la posición **con** los anuncios empalmados hacen referencia a una posición diferente en una sesión futura. TVSDK proporciona métodos para recuperar la posición de reproducción al ignorar los anuncios empalmados.

1. Cuando el usuario sale de un vídeo, la aplicación recupera y guarda la posición en el vídeo.

   >[!TIP]
   >
   >No se incluyen las duraciones de los anuncios.

   Las pausas publicitarias pueden variar en cada sesión debido a patrones de anuncios, restricción de frecuencia, etc. La hora actual del vídeo en una sesión puede ser diferente en una sesión futura. Al guardar una posición en el vídeo, la aplicación recupera la hora local Utilice el  `localTime` para leer esta posición , que puede guardar en el dispositivo o en una base de datos del servidor.

   Por ejemplo, si el usuario se encuentra en el minuto 20 del vídeo y esta posición incluye cinco minutos de anuncios, `currentTime` será de 1200 segundos, mientras que `localTime` en esta posición serán 900 segundos.

   >[!IMPORTANT]
   >
   >La hora local y la hora actual son las mismas para los flujos en directo/lineales. En este caso, `convertToLocalTime` no tiene ningún efecto. En VOD, la hora local permanece sin cambios mientras se reproducen los anuncios.

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

1. Para reanudar el vídeo en la misma posición que se guardó en la sesión anterior, utilice `seekToLocalTime`.

   >[!TIP]
   >
   >Solo se llama a este método con valores de hora local. Si se llama al método con los resultados de la hora actual, se produce un comportamiento incorrecto.

   Para buscar la hora actual, utilice `seekToTime`.

1. Cuando su aplicación reciba la `PTMediaPlayerStatusReady` evento de cambio de estado, busque la hora local guardada.

   ```
   [self.player seekToLocalTime:CMTimeMake(900, 1) completionHandler:^(BOOL finished) { 
       [self.player play]; 
   }];
   ```

1. Proporcione los saltos de anuncio según se especifican en la interfaz de la política de anuncios.
1. Implemente un selector de políticas de publicidad personalizado ampliando el selector de políticas de publicidad predeterminado.
1. Proporcione las pausas publicitarias que deben presentarse al usuario implementando `selectAdBreaksToPlay`

   >[!NOTE]
   >
   >Este método incluye una pausa publicitaria pre-roll y las pausas publicitarias mid-roll antes de la posición horaria local. La aplicación puede decidir reproducir una pausa publicitaria pre-roll y reanudarla a la hora local especificada, reproducir una pausa publicitaria mid-roll y reanudarla a la hora local especificada o reproducir ninguna pausa publicitaria.
