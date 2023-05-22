---
description: La interfaz PTMediaPlayer encapsula la funcionalidad y el comportamiento de un objeto de reproductor de contenidos.
title: Configuración de PTMediaPlayer
exl-id: 6d16bfd2-8d1d-4261-b343-c2e999c4d28b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# Configuración de PTMediaPlayer {#set-up-the-ptmediaplayer}

TVSDK proporciona herramientas para crear una aplicación de reproductor de vídeo avanzada (su reproductor Primetime) que puede integrar con otros componentes de Primetime.

Utilice las herramientas de su plataforma para crear un reproductor y conectarlo a la vista del reproductor de medios en TVSDK, que tiene métodos para reproducir y administrar vídeos. Por ejemplo, TVSDK proporciona métodos de reproducción y pausa. Puede crear botones de interfaz de usuario en la plataforma y establecer los botones para llamar a esos métodos de TVSDK.

La interfaz PTMediaPlayer encapsula la funcionalidad y el comportamiento de un objeto de reproductor de contenidos.

Para configurar su `PTMediaPlayer`:

1. Recupere la URL del contenido desde la interfaz de usuario, por ejemplo, en un campo de texto.

   ```
   NSURL *url = [NSURL URLWithString:textFieldURL.text];
   ```

1. Crear `PTMetadata`.

   Supongamos que su método `createMetada` prepara los metadatos (consulte [Publicidad](../../ios-3x-advertising/ios-3x-advertising-requirements.md)).

   ```
   PTMetadata *metadata = [self createMetadata]
   ```

1. Crear `PTMediaPlayerItem` mediante el uso de `PTMetadata` ejemplo.

   ```
   PTMediaPlayerItem *item = [[[PTMediaPlayerItem alloc] 
          initWithUrl:url mediaId:yourMediaID metadata:metadata] autorelease];
   ```

1. Añada observadores a las notificaciones que envía TVSDK.

   ```
   [self addObservers]
   ```

1. Crear `PTMediaPlayer` uso del nuevo `PTMediaPlayerItem`.

   ```
   PTMediaPlayer *player = [PTMediaPlayer playerWithMediaPlayerItem:item];
   ```

1. Establezca las propiedades en el reproductor.

   Estas son algunas de las disponibles `PTMediaPlayer` propiedades:

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

1. Agregar la vista del reproductor en la vista secundaria de la vista actual.

   ```
   [self.adPlayerView  setAutoresizesSubviews:YES];  
   [self.adPlayerView addSubview:(UIView *)player.view];
   ```

1. Llamada `play` para iniciar la reproducción de contenido.

   ```
   [player play];
   ```
