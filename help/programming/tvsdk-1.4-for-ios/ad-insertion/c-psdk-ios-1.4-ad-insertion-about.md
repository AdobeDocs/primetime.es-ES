---
description: La inserción de anuncios resuelve anuncios para vídeo a petición (VOD), para flujo continuo en directo y para flujo continuo lineal con seguimiento de anuncios y reproducción de anuncios. TVSDK realiza las solicitudes necesarias al servidor de publicidad, recibe información sobre las publicidades del contenido especificado y coloca las publicidades en el contenido en fases.
seo-description: La inserción de anuncios resuelve anuncios para vídeo a petición (VOD), para flujo continuo en directo y para flujo continuo lineal con seguimiento de anuncios y reproducción de anuncios. TVSDK realiza las solicitudes necesarias al servidor de publicidad, recibe información sobre las publicidades del contenido especificado y coloca las publicidades en el contenido en fases.
seo-title: Insertar publicidades
title: Insertar publicidades
uuid: 6fffb340-65ea-4c47-a55b-c0ec4917d37c
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 0%

---


# Insertar publicidades{#insert-ads}

La inserción de anuncios resuelve anuncios para vídeo a petición (VOD), para flujo continuo en directo y para flujo continuo lineal con seguimiento de anuncios y reproducción de anuncios. TVSDK realiza las solicitudes necesarias al servidor de publicidad, recibe información sobre las publicidades del contenido especificado y coloca las publicidades en el contenido en fases.

Una *`ad break`* publicación contiene una o más publicidades que se reproducen en secuencia. TVSDK inserta las publicidades en el contenido principal como miembros de uno o varios saltos de publicidad.

>[!TIP]
>
>Si la publicidad tiene errores, TVSDK la ignora.

## Resolver e insertar anuncios de VOD {#section_157344F857C64F36B48AD441F6E7FABA}

TVSDK admite varios casos de uso para la resolución e inserción de anuncios de VOD.

* Inserción previa de publicidad, donde las publicidades se insertan al principio del contenido.
* Inserción de anuncio intermedia, donde se inserta al menos un anuncio en medio del contenido.
* Inserción de anuncio posterior, donde al menos una publicidad se anexa al final del contenido.

TVSDK resuelve las publicidades, inserta las publicidades en ubicaciones definidas por el servidor de publicidad y calcula la línea de tiempo virtual antes de los inicios de reproducción. Después de los inicios de reproducción, no se pueden producir cambios, como anuncios insertados o insertados que se eliminan.

## Resolver e insertar anuncios en directo y lineales {#section_A6A1BB262D084462A1D134083556B7CC}

TVSDK admite varios casos de uso para la resolución e inserción de anuncios en directo y lineal.

* Inserción previa de publicidad, donde al menos se inserta una publicidad al principio del contenido.
* Inserción de anuncio intermedia, donde se inserta al menos un anuncio en medio del contenido.

TVSDK resuelve los anuncios e inserta los anuncios cuando se encuentra un punto de referencia en el flujo en directo o lineal. De forma predeterminada, TVSDK admite las siguientes indicaciones como marcadores de publicidad válidos al resolver y colocar publicidades:

* # EXT-X-CUEPOINT
* # EXT-X-AD
* # EXT-X-CUE
* # EXT-X-CUE-OUT

Estos marcadores requieren el campo de metadatos `DURATION` en segundos y el ID exclusivo de la señal. Por ejemplo:

```
#EXT-X-CUE DURATION=27 ID=identiferForThisCue ... 
```

Para obtener más información sobre las indicaciones adicionales, consulte [Suscripción a etiquetas](../ad-insertion/c-psdk-ios-1.4-custom-tags-configure/t-psdk-ios-1.4-custom-tags-subscribe.md)personalizadas.

## Rastrear la publicidad del cliente {#section_12355C7A35F14C15A2A18AAC90FEC2F5}

TVSDK rastrea automáticamente las publicidades para VOD y flujo en directo/lineal.

Las notificaciones se utilizan para informar a la aplicación sobre el progreso de una publicidad, incluida la información sobre cuándo comienza y cuándo finaliza una publicidad.

## Implementar un retorno de pausa publicitaria anticipado {#section_EEB9FE62CA7E4790B58D3CA906F43DCF}

Para la inserción de anuncios en directo, es posible que tenga que salir de una pausa publicitaria antes de que todas las publicidades del desglose se reproduzcan hasta la finalización.

Estos son algunos ejemplos de un retorno de pausa publicitaria anticipado:

* Duración de la pausa publicitaria en determinados eventos deportivos.

   Aunque se proporciona una duración predeterminada, si el juego se reanuda antes de que finalice la pausa, la pausa publicitaria debe salir.
* Una señal de emergencia durante una pausa publicitaria en un flujo en directo.

La capacidad de salir de una pausa publicitaria antes se identifica mediante una etiqueta personalizada en el manifiesto conocida como un empalme o una etiqueta de inicio. TVSDK permite a la aplicación suscribirse a estas etiquetas de empalme para proporcionar una oportunidad de empalme.

* Para utilizar la `#EXT-X-CUE-IN` etiqueta como una oportunidad de empalme e implementar un retorno de pausa publicitaria temprano:

   1. Suscríbase a la etiqueta .

      ```
      [PTSDKConfig setSubscribedTags:[NSArray arrayWithObject:@"#EXT-X-CUE-IN"]];
      ```

   1. Añada la resolución de la oportunidad de inicio de sesión.

      ```
      // self.player is the PTMediaPlayer instance created for content and ad playback 
      PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
      
      // Set cue in opportunity resolver 
      [clientFactory registerOpportunityResolver:[PTDefaultAdSpliceInOpportunityResolver adSpliceInOpportunityResolverWithTag:@"#EXT-X-CUE-IN"]];
      ```

* Para compartir la misma etiqueta para salir y empalmar:

   1. Si la aplicación está compartiendo la misma señal para indicar el cue-out/splice-out y el cue-in/splice-in, extienda `PTDefaultAdOpportunityResolver` e implemente el `preparePlacementOpportunity` método.

      >[!TIP]
      >
      >El código siguiente supone que la aplicación tiene una implementación para el `isCueInOpportunity` método.
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

   1. Registre la resolución de oportunidad extendida en la `PTDefaultMediaPlayerClientFactory` instancia.

      ```
      // self.player is the PTMediaPlayer instance created for content and ad playback 
      PTDefaultMediaPlayerClientFactory *clientFactory = self.player.mediaPlayerClientFactory; 
      
      // Clear existing resolver and register the new opportunity resolver 
      [clientFactory clearOpportunityResolvers]; 
      [clientFactory registerOpportunityResolver:[[PTDefaultExtendedAdOpportunityResolver new] autorelease]];
      ```

