---
description: La inserción de publicidad resuelve los anuncios para vídeo bajo demanda (VOD) , para flujo continuo en directo y para flujo lineal con seguimiento de anuncios y reproducción de anuncios. TVSDK realiza las solicitudes necesarias al servidor de publicidad, recibe información sobre las publicidades del contenido especificado y coloca las publicidades en el contenido por fases.
title: Insertar publicidades
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---


# Insertar anuncios{#insert-ads}

La inserción de publicidad resuelve los anuncios para vídeo bajo demanda (VOD) , para flujo continuo en directo y para flujo lineal con seguimiento de anuncios y reproducción de anuncios. TVSDK realiza las solicitudes necesarias al servidor de publicidad, recibe información sobre las publicidades del contenido especificado y coloca las publicidades en el contenido por fases.

Un *`ad break`* contiene uno o más anuncios que se reproducen en secuencia. TVSDK inserta anuncios en el contenido principal como miembros de una o más pausas publicitarias.

>[!TIP]
>
>Si el anuncio tiene errores, TVSDK ignora el anuncio.

## Resolver e insertar anuncios de VOD {#section_157344F857C64F36B48AD441F6E7FABA}

TVSDK admite varios casos de uso para la resolución e inserción de anuncios de VOD.

* Inserción de anuncio pre-roll, donde los anuncios se insertan al principio del contenido.
* Inserción de anuncio mid-roll, donde se inserta al menos un anuncio en medio del contenido.
* Inserción de anuncio posterior a la emisión, donde se anexa al final del contenido al menos un anuncio.

TVSDK resuelve los anuncios, los inserta en ubicaciones definidas por el servidor de publicidad y calcula la cronología virtual antes de que comience la reproducción. Una vez que comienza la reproducción, no se pueden producir cambios, como insertarse o eliminar anuncios insertados.

## Resuelva e inserte anuncios en vivo y lineales {#section_A6A1BB262D084462A1D134083556B7CC}

TVSDK admite varios casos de uso para la resolución y la inserción de anuncios en directo y lineal.

* Inserción de anuncio previo a la emisión, donde se inserta al menos un anuncio al principio del contenido.
* Inserción de anuncio mid-roll, donde se inserta al menos un anuncio en medio del contenido.

TVSDK resuelve los anuncios e inserta los anuncios cuando se encuentra un punto de referencia en el flujo en directo o lineal. De forma predeterminada, TVSDK admite las siguientes indicaciones como marcadores de publicidad válidos al resolver y colocar anuncios:

* # EXT-X-CUEPOINT
* # EXT-X-AD
* # EXT-X-CUE
* # EXT-X-CUE-OUT

Estos marcadores requieren el `DURATION` en segundos del campo de metadatos y el ID exclusivo del cue. Por ejemplo:

```
#EXT-X-CUE DURATION=27 ID=identiferForThisCue ... 
```

Para obtener más información sobre sugerencias adicionales, consulte [Suscribirse a etiquetas personalizadas](../ad-insertion/c-psdk-ios-1.4-custom-tags-configure/t-psdk-ios-1.4-custom-tags-subscribe.md).

## Seguimiento del anuncio de cliente {#section_12355C7A35F14C15A2A18AAC90FEC2F5}

TVSDK rastrea automáticamente los anuncios para VOD y flujo en directo/lineal.

Las notificaciones se utilizan para informar a la aplicación del progreso de una publicidad, incluida la información sobre cuándo comienza y cuándo finaliza una publicidad.

## Implementar un retorno de pausa publicitaria anticipado {#section_EEB9FE62CA7E4790B58D3CA906F43DCF}

Para la inserción de anuncios en directo, es posible que tenga que salir de una pausa publicitaria antes de que todos los anuncios de la pausa se reproduzcan hasta el final.

Estos son algunos ejemplos de un retorno anticipado de pausa publicitaria:

* Duración de la pausa publicitaria en determinados eventos deportivos.

   Aunque se proporciona una duración predeterminada, si el juego se reanuda antes de que finalice la pausa publicitaria, esta debe salir.
* Señal de emergencia durante una pausa publicitaria en una emisión en directo.

La capacidad de salir de una pausa publicitaria anticipadamente se identifica mediante una etiqueta personalizada en el manifiesto conocida como empalme o etiqueta de inclusión. TVSDK permite que la aplicación se suscriba a estas etiquetas de complemento para proporcionar una oportunidad de complemento.

* Para utilizar la etiqueta `#EXT-X-CUE-IN` como una oportunidad de inicio de secuencia e implementar un retorno de pausa publicitaria anticipado:

   1. Suscríbase a la etiqueta .

      ```
      [PTSDKConfig setSubscribedTags:[NSArray arrayWithObject:@"#EXT-X-CUE-IN"]];
      ```

   1. Añada la resolución de oportunidad de cue-in.

      ```
      // self.player is the PTMediaPlayer instance created for content and ad playback 
      PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
      
      // Set cue in opportunity resolver 
      [clientFactory registerOpportunityResolver:[PTDefaultAdSpliceInOpportunityResolver adSpliceInOpportunityResolverWithTag:@"#EXT-X-CUE-IN"]];
      ```

* Para compartir la misma etiqueta para el empalme y el empalme:

   1. Si la aplicación está compartiendo el mismo cue para indicar cue-out/splice-out y cue-in/splice-in, amplíe `PTDefaultAdOpportunityResolver` e implemente el método `preparePlacementOpportunity`.

      >[!TIP]
      >
      >El siguiente código supone que la aplicación tiene una implementación para el método `isCueInOpportunity` .
      >
      >
      ```
      >- (PTPlacementOpportunity *)preparePlacementOpportunity:(PTTimedMetadata *)timedMetadata 
      >{ 
      >       if ([self isCueInOpportunity:timedMetadata]) 
      >       { 
      >               return [PTPlacementOpportunity advertisementSpliceInOpportunityWithTimedMetadata:timedMetadata]; 
      >       } 
      >       else 
      >       { 
      >               return [super preparePlacementOpportunity:timedMetadata]; 
      >       } 
      >}
      >```

   1. Registre la resolución de oportunidad extendida en la instancia `PTDefaultMediaPlayerClientFactory` .

      ```
      // self.player is the PTMediaPlayer instance created for content and ad playback 
      PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
      
      // Clear existing resolver and register the new opportunity resolver 
      [clientFactory clearOpportunityResolvers]; 
      [clientFactory registerOpportunityResolver:[[PTDefaultExtendedAdOpportunityResolver new] autorelease]];
      ```

