---
description: La inserción de anuncios resuelve los anuncios para vídeo bajo demanda (VOD) , para flujo en directo y para flujo lineal con seguimiento de anuncios y reproducción de anuncios. TVSDK realiza las solicitudes necesarias al servidor de publicidad, recibe información sobre los anuncios del contenido especificado y coloca los anuncios en el contenido por fases.
title: Inserción de anuncios
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 0%

---

# Inserción de anuncios{#insert-ads}

La inserción de anuncios resuelve los anuncios para vídeo bajo demanda (VOD) , para flujo en directo y para flujo lineal con seguimiento de anuncios y reproducción de anuncios. TVSDK realiza las solicitudes necesarias al servidor de publicidad, recibe información sobre los anuncios del contenido especificado y coloca los anuncios en el contenido por fases.

Un *`ad break`* contiene uno o más anuncios que se reproducen en secuencia. TVSDK inserta anuncios en el contenido principal como miembros de una o más pausas publicitarias.

>[!TIP]
>
>Si el anuncio tiene errores, TVSDK ignora el anuncio.

## Resolución e inserción de anuncios de VOD {#section_157344F857C64F36B48AD441F6E7FABA}

TVSDK admite varios casos de uso para la resolución e inserción de anuncios de VOD.

* Inserción de anuncio previo a la emisión, donde los anuncios se insertan al principio del contenido.
* Inserción de anuncio durante la emisión, en la que se inserta al menos un anuncio en medio del contenido.
* Inserción de anuncio posterior a la emisión, donde al menos un anuncio se anexa al final del contenido.

TVSDK resuelve los anuncios, los inserta en ubicaciones definidas por el servidor de publicidad y calcula la cronología virtual antes de que se inicie la reproducción. Una vez iniciada la reproducción, no podrá producirse ningún cambio, como la inserción de anuncios o la eliminación de anuncios insertados.

## Resolución e inserción de publicidad lineal y en directo {#section_A6A1BB262D084462A1D134083556B7CC}

TVSDK admite varios casos de uso para la resolución e inserción de anuncios lineales y activos.

* Inserción de anuncio previo a la emisión, donde se inserta al menos un anuncio al principio del contenido.
* Inserción de anuncio durante la emisión, en la que se inserta al menos un anuncio en medio del contenido.

TVSDK resuelve los anuncios e inserta los anuncios cuando se encuentra un punto de referencia en el flujo en directo o lineal. De forma predeterminada, TVSDK admite las siguientes señales como marcadores de publicidad válidos al resolver y colocar anuncios:

* #EXT-X-CUEPOINT
* #EXT-X-AD
* #EXT-X-CUE
* #EXT-X-CUE-OUT

Estos marcadores requieren el campo de metadatos de `DURATION` en segundos y el ID único de la señal. Por ejemplo:

```
#EXT-X-CUE DURATION=27 ID=identiferForThisCue ... 
```

Para obtener más información sobre indicaciones adicionales, consulte [Suscripción a etiquetas personalizadas](../ad-insertion/c-psdk-ios-1.4-custom-tags-configure/t-psdk-ios-1.4-custom-tags-subscribe.md).

## Seguimiento del anuncio del cliente {#section_12355C7A35F14C15A2A18AAC90FEC2F5}

TVSDK realiza automáticamente un seguimiento de los anuncios para VOD y flujo en directo/lineal.

Las notificaciones se utilizan para informar a la aplicación sobre el progreso de un anuncio, incluida la información sobre cuándo comienza y cuándo termina un anuncio.

## Implementar un retorno de pausa publicitaria anticipado {#section_EEB9FE62CA7E4790B58D3CA906F43DCF}

Para la inserción de anuncios de flujo en directo, es posible que tenga que salir de una pausa publicitaria antes de que se reproduzcan todos los anuncios de la pausa hasta su finalización.

Estos son algunos ejemplos de retorno anticipado de una pausa publicitaria:

* La duración de la pausa publicitaria en determinados eventos deportivos.

  Aunque se proporciona una duración predeterminada, si el juego se reanuda antes de que finalice la pausa publicitaria, esta debe cerrarse.
* Una señal de emergencia durante una pausa publicitaria en una emisión en directo.

La capacidad de salir de una pausa publicitaria antes de tiempo se identifica mediante una etiqueta personalizada en el manifiesto conocida como etiqueta de entrada o de entrada. TVSDK permite que la aplicación se suscriba a estas etiquetas de empalme para proporcionar una oportunidad de empalme.

* Para usar la variable `#EXT-X-CUE-IN` etiquete como una oportunidad de integración e implemente una pausa publicitaria temprana:

   1. Suscríbase a la etiqueta.

      ```
      [PTSDKConfig setSubscribedTags:[NSArray arrayWithObject:@"#EXT-X-CUE-IN"]];
      ```

   1. Añada la resolución de la oportunidad de entrada.

      ```
      // self.player is the PTMediaPlayer instance created for content and ad playback 
      PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
      
      // Set cue in opportunity resolver 
      [clientFactory registerOpportunityResolver:[PTDefaultAdSpliceInOpportunityResolver adSpliceInOpportunityResolverWithTag:@"#EXT-X-CUE-IN"]];
      ```

* Para compartir la misma etiqueta para el empalme de salida y de entrada:

   1. Si la aplicación comparte la misma señal para indicar la salida/el empalme y la entrada/el empalme de entrada, amplíe `PTDefaultAdOpportunityResolver` e implementar el `preparePlacementOpportunity` método.

      >[!TIP]
      >
      >El siguiente código supone que la aplicación tiene una implementación para `isCueInOpportunity` método.
      >
      >```
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
      >

   1. Registre el solucionador de oportunidades extendido en la `PTDefaultMediaPlayerClientFactory` ejemplo.

      ```
      // self.player is the PTMediaPlayer instance created for content and ad playback 
      PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
      
      // Clear existing resolver and register the new opportunity resolver 
      [clientFactory clearOpportunityResolvers]; 
      [clientFactory registerOpportunityResolver:[[PTDefaultExtendedAdOpportunityResolver new] autorelease]];
      ```
