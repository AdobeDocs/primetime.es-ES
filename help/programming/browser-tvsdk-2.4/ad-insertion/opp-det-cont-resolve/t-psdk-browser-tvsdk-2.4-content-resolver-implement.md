---
description: Puede implementar sus propios resolvedores de contenido en función de los resolvedores predeterminados.
title: Implementación de una resolución de contenido personalizado
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 1%

---


# Implementar una resolución de contenido personalizada{#implement-a-custom-content-resolver}

Puede implementar sus propios resolvedores de contenido en función de los resolvedores predeterminados.

Cuando el TVSDK del explorador detecta una nueva oportunidad, se repite a través de los solucionadores de contenido registrados que buscan uno que sea capaz de resolver esa oportunidad usando el método `canResolve`. El primero que devuelve true se selecciona para resolver la oportunidad. Si no se puede resolver ningún contenido, se omite esa oportunidad. Dado que el proceso de resolución de contenido suele ser asíncrono, la resolución de contenido es responsable de notificar al TVSDK del explorador cuando el proceso ha finalizado.

Recuerde la siguiente información:

* La resolución de contenido llama a `client.process` para especificar qué operación de cronología debe ejecutar TVSDK.

   La operación suele ser una colocación de pausa publicitaria.

* La resolución de contenido llama a `client.notifyCompleted` si el proceso de resolución es exitoso o `client.notifyFailed` si falla el proceso.

1. Cree una resolución de oportunidad personalizada.

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

1. Cree la fábrica de contenido personalizado, que utiliza la resolución de contenido personalizado.

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

1. Registre la fábrica de contenido personalizado para la reproducción del flujo de medios.

   En el reproductor de UI Framework, puede especificar la fábrica de contenido personalizado de la siguiente manera:

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

