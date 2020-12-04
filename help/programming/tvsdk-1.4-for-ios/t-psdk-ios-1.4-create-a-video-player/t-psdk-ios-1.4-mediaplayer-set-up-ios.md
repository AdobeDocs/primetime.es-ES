---
description: La interfaz PTMediaPlayer encapsula la funcionalidad y el comportamiento de un objeto de reproductor de medios.
seo-description: La interfaz PTMediaPlayer encapsula la funcionalidad y el comportamiento de un objeto de reproductor de medios.
seo-title: Configuración de PTMediaPlayer
title: Configuración de PTMediaPlayer
uuid: 78549406-7e33-4bca-a25e-1e433f6a75d7
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---


# Configure PTMediaPlayer {#set-up-the-ptmediaplayer}

TVSDK proporciona herramientas para crear una aplicación de reproductor de vídeo avanzada (el reproductor Primetime), que se puede integrar con otros componentes de Primetime.

Utilice las herramientas de la plataforma para crear un reproductor y conectarlo a la vista del reproductor de medios en TVSDK, que dispone de métodos para reproducir y administrar vídeos. Por ejemplo, TVSDK proporciona métodos de reproducción y pausa. Puede crear botones de interfaz de usuario en la plataforma y definir los botones para llamar a esos métodos de TVSDK.

La interfaz PTMediaPlayer encapsula la funcionalidad y el comportamiento de un objeto de reproductor de medios.

Para configurar su `PTMediaPlayer`:

1. Obtenga la URL del medio desde la interfaz de usuario, por ejemplo, en un campo de texto.

   ```
   NSURL *url = [NSURL URLWithString:textFieldURL.text];
   ```

1. Crear `PTMetadata`.

   Supongamos que el método `createMetada` prepara metadatos (consulte [Publicidad](../ad-insertion/r-psdk-ios-1.4-advertising-requirements.md)).

   ```
   PTMetadata *metadata = [self createMetadata]
   ```

1. Cree `PTMediaPlayerItem` mediante la instancia `PTMetadata`.

   ```
   PTMediaPlayerItem *item = [[[PTMediaPlayerItem alloc] 
          initWithUrl:url mediaId:yourMediaID metadata:metadata] autorelease];
   ```

1. Añada observadores a las notificaciones que TVSDK distribuye.

   ```
   [self addObservers]
   ```

1. Cree `PTMediaPlayer` con su nuevo `PTMediaPlayerItem`.

   ```
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:item];
   ```

1. Configure las propiedades en el reproductor.

   Estas son algunas de las propiedades `PTMediaPlayer` disponibles:

   ```
   player.autoPlay                    = YES;  
   player.closedCaptionDisplayEnabled = YES; 
   player.videoGravity                = PTMediaPlayerVideoGravityResizeAspect;  
   player.allowsAirPlayVideo          = YES;
   ```

1. Establezca la propiedad de vista del reproductor.

   ```
   CGRect playerRect = self.adPlayerView.frame;  
   playerRect.origin = CGPointMake(0, 0); 
   playerRect.size = CGSizeMake(self.adPlayerView.frame.size.width,  
                                self.adPlayerView.frame.size.height); 
   
   [player.view setFrame:playerRect]; 
   [player.view setAutoresizingMask:  
         ( UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight )];
   ```

1. Añada la vista del reproductor en la subvista de la vista actual.

   ```
   [self.adPlayerView  setAutoresizesSubviews:YES];  
   [self.adPlayerView addSubview:(UIView *)player.view];
   ```

1. Llame a `play` para reproducir medios de inicio.

   ```
   [player play];
   ```

