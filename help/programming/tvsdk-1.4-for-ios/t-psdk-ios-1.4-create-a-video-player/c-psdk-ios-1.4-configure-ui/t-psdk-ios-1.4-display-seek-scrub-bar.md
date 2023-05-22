---
description: Puede mostrar el tiempo actual y el tiempo restante del contenido que se está reproduciendo.
title: Mostrar una barra de desplazamiento de búsqueda con la posición de tiempo de reproducción actual
exl-id: a8b34cf4-4dfd-4799-9408-87c4d60eff4c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '62'
ht-degree: 0%

---

# Mostrar una barra de desplazamiento de búsqueda con la posición de tiempo de reproducción actual {#display-a-seek-scrub-bar-with-the-current-playback-time-position}

Puede mostrar el tiempo actual y el tiempo restante del contenido que se está reproduciendo.

Para implementar una barra de desplazamiento, utilice el siguiente código de ejemplo:

```
// 1. Register for the PTMediaPlayerTimeChangeNotification 
[[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerTimeChange:)  
  name:PTMediaPlayerTimeChangeNotification object:self.player]; 
 
... 
 
_positionSlider = [[UISlider alloc] initWithFrame:CGRectMake(105.0, 14.0, 370, 24)];  
[_positionSlider addTarget:self action:@selector(sliderThumbReleased:)  
  forControlEvents:UIControlEventTouchUpInside]; 
 
... 
 
// 2. Cover the event where the user moves to a different location in the stream 
- (void)sliderThumbReleased:(id)sender { 
    double  sliderTime = [_positionSlider  value];  
    CMTimeRange seekableRange = self.player.seekableRange; 
    if (CMTIMERANGE_IS_VALID(seekableRange)) { 
        double start = CMTimeGetSeconds(seekableRange.start);  
        double duration = CMTimeGetSeconds(seekableRange.duration); 
 
        CMTime newTime = CMTimeMakeWithSeconds((sliderTime * duration) + start, AD_TIMESCALE);  
        [self.player seekToTime:newTime]; 
    } 
} 
 
... 
 
// 3. This method is called whenever the player time changes  
(PTMediaPlayerTimeChangeNotification) 
- (void) onMediaPlayerTimeChange:(NSNotification *)notification { 
    CMTimeRange seekableRange = self.player.seekableRange; 
 
    if (CMTIMERANGE_IS_VALID(seekableRange)) { 
        double start = CMTimeGetSeconds(seekableRange.start);  
        double duration = CMTimeGetSeconds(seekableRange.duration); 
        double currentTime = CMTimeGetSeconds(self.player.currentItem.currentTime); 
 
        if (duration > 0) { 
            //Set the position slider value on the current playback time  
            [_positionSlider setValue:((currentTime - start) / duration)]; 
        } 
    } 
} 
```
