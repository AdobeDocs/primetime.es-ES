---
description: Puede implementar sus propias resoluciones de contenido en función de las resoluciones predeterminadas.
title: Implementación de un solucionador de contenido personalizado
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# Implementación de un solucionador de contenido personalizado{#implement-a-custom-content-resolver}

Puede implementar sus propias resoluciones de contenido en función de las resoluciones predeterminadas.

Cuando el TVSDK del explorador detecta una nueva oportunidad, se repite a través de los solucionadores de contenido registrados en busca de uno que sea capaz de resolver esa oportunidad mediante el uso del `canResolve` método. El primero que devuelve el valor &quot;True&quot; se selecciona para resolver la oportunidad. Si no hay ningún solucionador de contenido capaz, esa oportunidad se omite. Dado que el proceso de resolución de contenido suele ser asincrónico, el gestor de contenido es responsable de notificar al TVSDK del explorador cuando el proceso se haya completado.

Recuerde la siguiente información:

* El solucionador de contenido llama a `client.process` para especificar qué operación de cronología debe ejecutar TVSDK.

  La operación suele ser una colocación de pausa publicitaria.

* El solucionador de contenido llama a `client.notifyCompleted` si el proceso de resolución se ha realizado correctamente o `client.notifyFailed` si el proceso falla.

1. Cree una resolución de oportunidades personalizada.

   ```js
   /** 
     * Class implementing AdobePSDK.ContentResolver interface  
   */ 
   CustomResolver = function () { 
   }; 
   
   CustomResolver.prototype = { 
       constructor: CustomResolver, 
       configureCallbackFunc: function (item, client) { 
       // here you can read any media stream characteristics which 
       // might help configure your content resolver like 
       // - the media player item configuration through the item.config 
       // - the media resource metadata through item.resource.metadata 
      }, 
   
       canResolveCallbackFunc: function (opportunity) { 
       // check if the opportunity can be resolved by this resolver 
       // if yes return true, otherwise return false 
       return true; 
      }, 
   
       resolveCallbackFunc: function (opportunity) {         
       // start the resolving process 
       // communicate with your custom ad server 
   
       // in this example we assume that: 
       // - if successful, onResolveCompleted method will be invoked 
       // - if failed, onResolveFailed method will be invoked 
      }, 
   
       onResolveCompleted: function (response) { 
        try { 
           var proposals = []; 
           // extract the timeline ad placement from the response 
           // and add them to the proposal vector 
           // - extract the ad break 
           // - calculate the placement (can reuse the _opportunity.placement) 
           // var timelineOperation = new AdobePSDK.AdBreakPlacement (adBreak, placement); 
           // proposals.push (timelineOperation); 
   
           client.process (proposals); 
           client.notifyCompleted (_opportunity); 
       } catch (error) { 
           onResolveFailed (error); 
       } 
   }, 
   
       onResolveFailed: function (error) { 
         client.notifyFailed (_opportunity); 
       } 
   
   }; 
   ```

1. Cree la fábrica de contenido personalizado, que utiliza la resolución de contenido personalizada.

   Por ejemplo:

   ```js
   /** 
     * Class implementing AdobePSDK.ContentFactory interface 
   */ 
   CustomContentFactory = function () { 
   }; 
   
   CustomContentFactory.prototype = { 
       constructor: CustomContentFactory, 
       retrieveResolversCallbackFunc: function (item) { 
           var result = []; 
           var resource = item.resource; 
           if (resource.metadata.containsKey("custom-opportunity-detector")) { 
               result.push (new CustomResolver()); 
           } 
           return result; 
       }, 
       … 
   }; 
   ```

1. Registre la fábrica de contenido personalizado para el flujo de medios que se va a reproducir.

   En el reproductor del marco de trabajo de la interfaz de usuario, puede especificar la fábrica de contenido personalizado de la siguiente manera:

   ```js
   var advertisingFactory = new CustomContentFactory(); 
   var advertisingMetadata = new AdobePSDK.AdvertisingMetadata(); 
   // set any parameter you need for custom ad resolver 
   // advertisingMetadata.setValue ("customparam", "customvalue"); 
   
   var metadata = new AdobePSDK.Metadata(); 
   metadata.setMetadata ("custom-opportunity-detector", advertisingMetadata); 
   
   var playerWrapper = ptp.videoPlayer('.videoDiv', { 
    player: { 
       mediaPlayerItemConfig: { 
              advertisingFactory: advertisingFactory 
       }, 
          mediaResource: { 
                  resourceUrl:'Specify Resource Url', 
                  metadata: metadata 
          } 
   } 
   
   }); 
   ```
