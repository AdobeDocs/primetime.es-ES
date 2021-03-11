---
description: La interfaz de PTMediaPlayer encapsula la funcionalidad y el comportamiento de un objeto de reproductor multimedia.
title: Configuración de PTMediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# Configuración de PTMediaPlayer {#set-up-the-ptmediaplayer}

TVSDK proporciona herramientas para crear una aplicación de reproductor de vídeo avanzada (su reproductor Primetime), que puede integrar con otros componentes de Primetime.

Utilice las herramientas de su plataforma para crear un reproductor y conectarlo a la vista del reproductor de medios en TVSDK, que tiene métodos para reproducir y administrar vídeos. Por ejemplo, TVSDK proporciona métodos de reproducción y pausa. Puede crear botones de interfaz de usuario en la plataforma y establecer los botones para llamar a esos métodos de TVSDK.

La interfaz de PTMediaPlayer encapsula la funcionalidad y el comportamiento de un objeto de reproductor multimedia.

Para configurar su `PTMediaPlayer`:

1. Busque la URL del medio en la interfaz de usuario, por ejemplo, en un campo de texto.

   ```
   NSURL *url = [NSURL URLWithString:textFieldURL.text];
   ```

1. Crear `PTMetadata`.

   Supongamos que el método `createMetada` prepara metadatos (consulte [Publicidad](../../ios-3x-advertising/ios-3x-advertising-requirements.md)).

   ```
   PTMetadata *metadata = [self createMetadata]
   ```

1. Cree `PTMediaPlayerItem` usando la instancia `PTMetadata`.

   ```
   PTMediaPlayerItem *item = [[[PTMediaPlayerItem alloc] 
          initWithUrl:url mediaId:yourMediaID metadata:metadata] autorelease];
   ```

1. Agregue observadores a las notificaciones que envía TVSDK.

   ```
   [self addObservers]
   ```

1. Cree `PTMediaPlayer` con su nuevo `PTMediaPlayerItem`.

   ```
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:item];
   ```

1. Establezca propiedades en el reproductor.

   Estas son algunas de las propiedades `PTMediaPlayer` disponibles:

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

1. Invoque `play` para iniciar la reproducción del contenido.

   ```
   [player play];
   ```
