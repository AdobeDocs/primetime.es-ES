---
description: Puede implementar las resoluciones en función de las resoluciones predeterminadas.
title: Implementación de un solucionador de contenido/oportunidad personalizado
exl-id: f2a8512f-9f6c-4fd9-8694-32132cddc7d2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 0%

---

# Implementación de un solucionador de contenido/oportunidad personalizado{#implement-a-custom-opportunity-content-resolver}

Puede implementar las resoluciones en función de las resoluciones predeterminadas.

<!--<a id="fig_CC41E2A66BDB4115821F33737B46A09B"></a>-->

![](assets/ios_psdk_content_resolver.png)

1. Desarrollar un solucionador de anuncios personalizado ampliando el `PTContentResolver` clase abstracta.

   `PTContentResolver` es una interfaz que debe implementar una clase de resolución de contenido. También hay disponible una clase abstracta con el mismo nombre y controla la configuración automáticamente (obteniendo el delegado).

   >[!TIP]
   >
   >`PTContentResolver` se expone a través de `PTDefaultMediaPlayerClientFactory` clase. Los clientes pueden registrar un nuevo solucionador de contenido ampliando el `PTContentResolver` clase abstracta. De forma predeterminada, y a menos que se elimine específicamente, una `PTDefaultAdContentResolver` está registrado en la `PTDefaultMediaPlayerClientFactory`.

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

1. Implementación `shouldResolveOpportunity` y volver `YES` si debe gestionar el `PTPlacementOpportunity`.
1. Implementación `resolvePlacementOpportunity`, que comienza a cargar el contenido alternativo o los anuncios.
1. Una vez cargados los anuncios, prepare un `PTTimeline` con la información sobre el contenido que se va a insertar.

       A continuación se proporciona información útil sobre las escalas de tiempo:
   
   * Puede haber varios `PTAdBreak`s de los tipos pre-roll, mid-roll y post-roll.

      * A `PTAdBreak` tiene lo siguiente:

         * A `CMTimeRange` con la hora de inicio y la duración de la pausa.

            Se establece como la propiedad de rango de `PTAdBreak`.

         * `NSArray` de `PTAd`s.

            Se establece como la propiedad ads de `PTAdBreak`.
   * A `PTAd` representa el anuncio, y cada `PTAd` tiene lo siguiente:

      * A `PTAdHLSAsset` establezca como propiedad de recurso principal de la publicidad.
      * Posiblemente múltiple `PTAdAsset` ejemplos como anuncios en los que se puede hacer clic o anuncios de banner.

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

1. Llamada `didFinishResolvingPlacementOpportunity`, que proporciona el `PTTimeline`.
1. Registre el solucionador de contenido/publicidad personalizado en la fábrica del reproductor de medios predeterminado llamando a `registerContentResolver`.

   ```
   //Remove default content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearContentResolvers]; 
   
   //Create an instance of your content/ad resolver (id <PTContentResolver>) 
   CustomContentResolver *contentResolver = [[CustomContentResolver alloc] init]; 
   
   //Set custom content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] registerContentResolver:[contentResolver autorelease]];
   ```

1. Si ha implementado una resolución de oportunidad personalizada, regístrela en la fábrica del reproductor de medios predeterminada.

   >[!TIP]
   >
   >No es necesario registrar un solucionador de oportunidad personalizado para registrar un solucionador de publicidad o contenido personalizado.

   ```
   //Remove default opportunity resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearOpportunityResolvers]; 
   
   //Create an instance of your opportunity resolver (id <PTOpportunityResolver>) 
   CustomOpportunityResolver *opportunityResolver = [[CustomOpportunityResolver alloc] init]; 
   
   //Set custom opportunity resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory]  
              registerOpportunityResolver:[opportunityResolver autorelease]];
   ```

Cuando el reproductor carga el contenido y se determina que es de tipo VOD o LIVE, se produce una de las siguientes situaciones: >
* Si el contenido es VOD, se utiliza la resolución de contenido personalizada para obtener la cronología de la publicidad de todo el vídeo.
* Si el contenido está ACTIVO, se llama al solucionador de contenido personalizado cada vez que se detecta una oportunidad de ubicación (punto de referencia) en el contenido.
