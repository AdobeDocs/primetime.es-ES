---
description: Puede implementar los solucionadores en función de los resueltores predeterminados.
seo-description: Puede implementar los solucionadores en función de los resueltores predeterminados.
seo-title: Implementar una solución de contenido/oportunidad personalizada
title: Implementar una solución de contenido/oportunidad personalizada
uuid: 0023f516-12f3-4548-93de-b0934789053b
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Implementar una solución de contenido/oportunidad personalizada {#implement-a-custom-opportunity-content-resolver}

Puede implementar los solucionadores en función de los resueltores predeterminados.

<!--<a id="fig_CC41E2A66BDB4115821F33737B46A09B"></a>-->

![](assets/ios_psdk_content_resolver.png)

1. Desarrolle una resolución de publicidad personalizada ampliando la clase `PTContentResolver` abstracta.

   `PTContentResolver` es una interfaz que debe ser implementada por una clase de resolución de contenido. También hay disponible una clase abstracta con el mismo nombre que gestiona la configuración automáticamente (obteniendo el delegado).

   >[!TIP]
   >
   >`PTContentResolver` se expone a través de la `PTDefaultMediaPlayerClientFactory` clase. Los clientes pueden registrar una nueva resolución de contenido ampliando la clase `PTContentResolver` abstracta. De forma predeterminada, y a menos que se elimine específicamente, `PTDefaultAdContentResolver` se registra un valor en la `PTDefaultMediaPlayerClientFactory`.

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

1. Implemente `shouldResolveOpportunity` y devuelva `YES` si debe gestionar la recepción `PTPlacementOpportunity`.
1. Implementar `resolvePlacementOpportunity`, que comienza a cargar el contenido o las publicidades alternativas.
1. Una vez cargadas las publicidades, prepare un `PTTimeline` archivo con la información sobre el contenido que se va a insertar.

       A continuación se ofrece información útil sobre las líneas de tiempo:
   
   * Puede haber varios tipos `PTAdBreak`de predesplazamiento, de media rodadura y de postrollo.

      * A `PTAdBreak` tiene lo siguiente:

         * Un `CMTimeRange` con la hora de inicio y la duración del salto.

            Se establece como la propiedad range de `PTAdBreak`.

         * `NSArray` de `PTAd`s.

            Se establece como la propiedad ads de `PTAdBreak`.
   * Un `PTAd` representa la publicidad y cada una `PTAd` de ellas tiene lo siguiente:

      * Un `PTAdHLSAsset` conjunto como propiedad de recurso principal de la publicidad.
      * Posiblemente varias `PTAdAsset` instancias como publicidades en titulares o publicidades en las que se puede hacer clic.
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

1. Llamada `didFinishResolvingPlacementOpportunity`, que proporciona la `PTTimeline`.
1. Registre la resolución de contenido y publicidad personalizada en la fábrica predeterminada del reproductor de medios llamando `registerContentResolver`.

   ```
   //Remove default content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] clearContentResolvers]; 
   
   //Create an instance of your content/ad resolver (id <PTContentResolver>) 
   CustomContentResolver *contentResolver = [[CustomContentResolver alloc] init]; 
   
   //Set custom content/ad resolver 
   [[PTDefaultMediaPlayerFactory defaultFactory] registerContentResolver:[contentResolver autorelease]];
   ```

1. Si ha implementado una resolución de oportunidades personalizada, regístrela en la fábrica de reproductores de medios predeterminada.

   >[!TIP]
   >
   >No es necesario registrar una resolución de oportunidades personalizada para registrar una resolución de contenido/publicidad personalizada.

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

* Si el contenido es VOD, la resolución de contenido personalizado se utiliza para obtener la línea de tiempo de publicidad de todo el vídeo.
* Si el contenido está ACTIVO, se llama a la resolución de contenido personalizado cada vez que se detecta una oportunidad de colocación (punto de referencia) en el contenido.