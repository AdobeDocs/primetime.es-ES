---
description: La interfaz PTMediaPlayer encapsula la funcionalidad y el comportamiento de un objeto de reproductor de medios.
seo-description: La interfaz PTMediaPlayer encapsula la funcionalidad y el comportamiento de un objeto de reproductor de medios.
seo-title: Configuración de PTMediaPlayer
title: Configuración de PTMediaPlayer
uuid: 698034d3-1260-416f-83b0-6b7d058750a0
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Configuración de PTMediaPlayer {#set-up-the-ptmediaplayer}

TVSDK proporciona herramientas para crear una aplicación de reproductor de vídeo avanzada (el reproductor Primetime), que se puede integrar con otros componentes de Primetime.

Utilice las herramientas de su plataforma para crear un reproductor y conectarlo a la vista del reproductor de medios en TVSDK, que dispone de métodos para reproducir y administrar vídeos. Por ejemplo, TVSDK proporciona métodos de reproducción y pausa. Puede crear botones de interfaz de usuario en la plataforma y definir los botones para llamar a esos métodos de TVSDK.

La interfaz PTMediaPlayer encapsula la funcionalidad y el comportamiento de un objeto de reproductor de medios.

Para configurar el `PTMediaPlayer`:

1. Obtenga la URL del medio desde la interfaz de usuario, por ejemplo, en un campo de texto.

   ```
   NSURL *url = [NSURL URLWithString:textFieldURL.text];
   ```

1. Crear `PTMetadata`.

   Supongamos que el método `createMetada` prepara metadatos (consulte [Publicidad](../../ios-3x-advertising/ios-3x-advertising-requirements.md)).

   ```
   PTMetadata *metadata = [self createMetadata]
   ```

1. Crear `PTMediaPlayerItem` usando la `PTMetadata` instancia.

   ```
   PTMediaPlayerItem *item = [[[PTMediaPlayerItem alloc] 
          initWithUrl:url mediaId:yourMediaID metadata:metadata] autorelease];
   ```

1. Agregue observadores a las notificaciones que distribuye TVSDK.

   ```
   [self addObservers]
   ```

1. Cree `PTMediaPlayer` con el nuevo `PTMediaPlayerItem`.

   ```
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:item];
   ```

1. Configure las propiedades en el reproductor.

   Estas son algunas de las `PTMediaPlayer` propiedades disponibles:

   ```
   player.autoPlay                    = YES;  
   player.closedCaptionDisplayEnabled = YES; 
   player.videoGravity                = PTMediaPlayerVideoGravityResizeAspect;  
   player.allowsAirPlayVideo          = YES;
   ```

1. Establezca la propiedad view del reproductor.

   ```
   CGRect playerRect = self.adPlayerView.frame;  
   playerRect.origin = CGPointMake(0, 0); 
   playerRect.size = CGSizeMake(self.adPlayerView.frame.size.width,  
                                self.adPlayerView.frame.size.height); 
   
   [player.view setFrame:playerRect]; 
   [player.view setAutoresizingMask:  
         ( UIViewAutoresizingFlexibleWidth | UIViewAutoresizingFlexibleHeight )];
   ```

1. Agregue la vista del reproductor en la subvista de la vista actual.

   ```
   [self.adPlayerView  setAutoresizesSubviews:YES];  
   [self.adPlayerView addSubview:(UIView *)player.view];
   ```

1. Llama `play` para iniciar la reproducción de medios.

   ```
   [player play];
   ```
