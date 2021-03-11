---
description: Puede implementar los resolvedores en función de los resolventes predeterminados.
title: Implementación de una oportunidad/resolución de contenido personalizada
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---


# Implementar una oportunidad/resolución de contenido personalizada {#implement-a-custom-opportunity-content-resolver}

Puede implementar los resolvedores en función de los resolventes predeterminados.

<!--<a id="fig_CC41E2A66BDB4115821F33737B46A09B"></a>-->

![](assets/ios_psdk_content_resolver.png)

1. Desarrolle una resolución de anuncios personalizada ampliando la clase abstracta `PTContentResolver`.

   `PTContentResolver` es una interfaz que debe ser implementada por una clase de resolución de contenido. También hay disponible una clase abstracta con el mismo nombre que gestiona la configuración automáticamente (obteniendo el delegado).

   >[!TIP]
   >
   >`PTContentResolver` se expone a través de la  `PTDefaultMediaPlayerClientFactory` clase . Los clientes pueden registrar una nueva resolución de contenido ampliando la clase abstracta `PTContentResolver`. De forma predeterminada, y a menos que se elimine específicamente, se registra un `PTDefaultAdContentResolver` en el `PTDefaultMediaPlayerClientFactory`.

   ```
   @protocol PTContentResolver <NSObject> 
   @required 
   + (BOOL)shouldHandleOpportunity:(PTPlacementOpportunity *)opportunity;  
   //Detector returns YES/NO if it should handle the following placement opportunity 
   - (void)configWithPlayerItem:(PTMediaPlayerItem *)item  
                 delegate:(id<PTContentResolverDelegate> delegate); 
   - (void)process:(PTPlacementOpportunity *)opportunity; 
   - (void)timeout:(PTPlacementOpportunity *)opportunity;  
   //The timeout method gets invoked if the TVSDK decides that the  
   //PTContentResolver is taking too much time to respond. 
   @end 
   
   @interface PTContentResolver : NSObject <PTContentResolver> 
   
   @property (readonly) id<PTContentResolverDelegate> delegate; 
   @property (readonly) PTMediaPlayerItem *playerItem; 
   
   - (BOOL)shouldHandleOpportunity:(PTPlacementOpportunity *)opportunity; 
   - (void)configWithPlayerItem:(PTMediaPlayerItem *)item  
                  delegate:(id<PTContentResolverDelegate>) delegate; 
   - (void)process:(NSArray *)opportunities; 
   - (void)cancel:(NSArray *)opportunities; 
   @end
   ```

1. Implemente `shouldResolveOpportunity` y devuelva `YES` si debe administrar el `PTPlacementOpportunity` recibido.
1. Implemente `resolvePlacementOpportunity`, que comienza a cargar el contenido o anuncios alternativos.
1. Una vez cargados los anuncios, prepare un `PTTimeline` con la información sobre el contenido que se va a insertar.

       A continuación se proporciona información útil sobre las cronologías:
   
   * Puede haber varios `PTAdBreak`s de tipos pre-roll, mid-roll y post-roll.

      * Una `PTAdBreak` tiene lo siguiente:

         * Un `CMTimeRange` con la hora de inicio y la duración de la pausa.

            Se establece como la propiedad range de `PTAdBreak`.

         * `NSArray` de  `PTAd`s.

            Se establece como la propiedad ads de `PTAdBreak`.
   * Un `PTAd` representa el anuncio y cada `PTAd` tiene lo siguiente:

      * Un `PTAdHLSAsset` establecido como propiedad de recurso principal del anuncio.
      * Posiblemente varias `PTAdAsset` instancias como anuncios en los que se puede hacer clic o anuncios en banners.

   Por ejemplo:

   ```
   NSMutableArray *ptBreaks = [[[NSMutableArray alloc] init] autorelease]; 
   
   // Prepare the primary asset of the ad - links to ad m3u8 
   PTAdHLSAsset *ptAdAsset = [[[PTAdHLSAsset alloc] init] autorelease]; 
   ptAdAsset.source = AD_SOURCE_M3U8; 
   ptAdAsset.id = FAKE_NUMBER_ID; 
   ptAdAsset.format = @"video"; 
   
   // Prepare the ad itself. 
   PTAd *ptAd = [[[PTAd alloc] init] autorelease]; 
   ptAd.primaryAsset = ptAdAsset; 
   ptAd.primaryAsset.ad = ptAd; 
   
   // Prepare the break and add the ad created above. 
   PTAdBreak *ptBreak = [[[PTAdBreak alloc] init] autorelease]; 
   ptBreak.relativeRange = CMTimeRangeMake(BREAK_START_TIME, BREAK_DURATION_VALUE); 
   [ptBreak addAd:ptAd]; 
   
   // Add the break to array of breaks. 
   [ptBreaks addObject:adBreak]; 
   
   // Once all breaks have been prepared, they can be set on timeline 
   PTTimeline *_timeline = [[PTTimeline alloc] init]; 
   _timeline.adBreaks = ptBreaks;
   ```

1. Llame a `didFinishResolvingPlacementOpportunity`, que proporciona el `PTTimeline`.
1. Registre la resolución de anuncios/contenido personalizado en la fábrica predeterminada del reproductor de medios llamando a `registerContentResolver`.

   ```
   //Remove default content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearContentResolvers]; 
   
   //Create an instance of your content/ad resolver (id <PTContentResolver>) 
   CustomContentResolver *contentResolver = [[CustomContentResolver alloc] init]; 
   
   //Set custom content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] registerContentResolver:[contentResolver autorelease]];
   ```

1. Si ha implementado una resolución de oportunidad personalizada, regístrela a la fábrica predeterminada del reproductor de medios.

   >[!TIP]
   >
   >No es necesario registrar un solucionador de oportunidades personalizado para registrar un solucionador de contenido/anuncios personalizado.

   ```
   //Remove default opportunity resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearOpportunityResolvers]; 
   
   //Create an instance of your opportunity resolver (id <PTOpportunityResolver>) 
   CustomOpportunityResolver *opportunityResolver = [[CustomOpportunityResolver alloc] init]; 
   
   //Set custom opportunity resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory]  
              registerOpportunityResolver:[opportunityResolver autorelease]];
   ```

Cuando el reproductor carga el contenido y se determina que es de tipo VOD o LIVE, se produce una de las siguientes situaciones:

* Si el contenido es VOD, la resolución de contenido personalizado se utiliza para obtener la cronología de anuncio de todo el vídeo.
* Si el contenido está ACTIVO, se llama a la resolución del contenido personalizado cada vez que se detecta una oportunidad de colocación (punto de referencia) en el contenido.