---
description: Puede configurar botones que llamen a los métodos TVSDK para pausar y reproducir el medio.
seo-description: Puede configurar botones que llamen a los métodos TVSDK para pausar y reproducir el medio.
seo-title: Implementar un botón de reproducción/pausa
title: Implementar un botón de reproducción/pausa
uuid: b0ce4103-819e-4a1c-8238-1d7728ec8770
translation-type: tm+mt
source-git-commit: a63768e51c911914a6ba9d884e2587fa34939f9d

---


# Implementar un botón de reproducción/pausa {#implement-a-play-pause-button}

Puede configurar botones que llamen a los métodos TVSDK para pausar y reproducir el medio.

Utilice el siguiente código de muestra para implementar un botón de reproducción o pausa:

<!--<a id="example_BC2632D673FE451190A30A23145090D0"></a>-->

```
_playPauseButton =  
[[UIButton alloc] initWithFrame:CGRectMake(BUTTON_POS_X, BUTTON_POS_Y, BUTTON_SIZE_W, BUTTON_SIZE_H)]; 
[_playPauseButton setImage:[UIImage imageNamed:@"play.png"] forState:UIControlStateNormal];  
[_playPauseButton setImage:[UIImage imageNamed:@"pause.png"] forState:UIControlStateSelected]; 
[_playPauseButton addTarget:self action:@selector(playTouch:) forControlEvents:UIControlEventTouchUpInside]; 
[self addSubview:_playPauseButton]; 
 
... 
 
- (void)playTouch:(id)sender { 
    if (self.player.status == PTMediaPlayerStatusPlaying) { 
        _playPauseButton.selected = YES;  
        [self.player pause]; 
    } 
    else { 
        _playPauseButton.selected = NO; [self.player play]; 
    } 
} 
```
