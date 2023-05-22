---
description: TVSDK admite anuncios de banner complementarios, que son anuncios que acompañan a un anuncio lineal y que a menudo permanecen en la página después de que finaliza el anuncio lineal. La aplicación es responsable de mostrar los titulares complementarios que se proporcionan con un anuncio lineal.
title: Anuncios de banner complementarios
exl-id: c10a38ec-acbb-4e84-aff2-c93c9b1cec81
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# Anuncios de banner complementarios {#companion-banner-ads}

TVSDK admite anuncios de banner complementarios, que son anuncios que acompañan a un anuncio lineal y que a menudo permanecen en la página después de que finaliza el anuncio lineal. La aplicación es responsable de mostrar los titulares complementarios que se proporcionan con un anuncio lineal.

Cuando muestre anuncios complementarios, siga estas recomendaciones:

* Intente presentar tantos anuncios de banner de vídeo como se ajusten al diseño del reproductor.
* Presente un banner complementario únicamente si tiene una ubicación que coincida exactamente con la altura y anchura especificadas.

   >[!TIP]
   >
   >No cambie el tamaño del titular.

* Presente los banners de acompañamiento lo antes posible después de que comience el anuncio.
* No superponga el contenedor de vídeo/anuncio principal con titulares complementarios.
* Continúe mostrando los titulares acompañantes una vez finalizado el anuncio.

   El estándar es mostrar cada banner complementario hasta que tenga un reemplazo para este banner.

## Datos de banner complementario {#companion-banner-data}

El contenido de un AdBannerAsset describe un banner complementario.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

El `AdPlaybackEvent.AD_STARTED` el evento devuelve un `Ad` instancia que contiene un `companionAssets` property ( `Vector.<AdAsset>`).
Cada `AdAsset` proporciona información sobre cómo mostrar el recurso.

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Información disponible </th> 
   <th colname="col2" class="entry"> Descripción </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> anchura </td> 
   <td colname="col2"> Anchura del banner complementario en píxeles. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> altura </td> 
   <td colname="col2"> Altura del banner complementario en píxeles. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> tipo de recurso </td> 
   <td colname="col2">El tipo de recurso para este banner complementario: 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html: los datos están en código de HTML. </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe: los datos son una dirección URL de iframe (src). </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> datos de banner </td> 
   <td colname="col2"> Los datos del tipo especificado por. <span class="codeph"> resourceType</span> para este banner complementario. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> URL estática </td> 
   <td colname="col2"> <p>A veces, el banner complementario también tiene una URL estática que es una URL directa a la imagen o a un <span class="filepath"> .swf</span> (titular de flash). </p> <p>Si no desea utilizar html o iframe, puede utilizar una URL directa a una imagen o swf para mostrar el titular en la fase de Flash en su lugar. En este caso, puede utilizar la dirección URL estática para mostrar el titular. </p> <p>Importante: Debe comprobar si la dirección URL estática es una cadena válida, ya que esta propiedad podría no estar siempre disponible. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Mostrar anuncios de banner {#display-banner-ads}

Para mostrar anuncios de banner, debe crear instancias de banner y permitir que TVSDK escuche eventos relacionados con anuncios.

TVSDK proporciona una lista de anuncios de banner complementarios asociados a un anuncio lineal a través de `AdPlaybackEvent.AD_STARTED` evento de evento.

Los manifiestos pueden especificar anuncios de banner complementarios mediante:

* Un fragmento de HTML
* La dirección URL de una página iFrame
* La URL de una imagen estática o un archivo del SWF del Flash de Adobe

Para cada anuncio complementario, TVSDK indica qué tipos están disponibles para su aplicación.

Agregue un oyente para `AdPlaybackEvent.AD_STARTED` que hace lo siguiente:

1. Borra los anuncios existentes en la instancia de banner.

1. Obtiene la lista de anuncios complementarios de `Ad.companionAssets`.

1. Si la lista de anuncios complementarios no está vacía, itere en la lista de instancias de banner.

   Cada instancia de banner ( y `AdBannerAsset`) contiene información, como anchura, altura, tipo de recurso (html, iframe o estático) y datos necesarios para mostrar el banner complementario.

1. Si un anuncio de vídeo no tiene anuncios complementarios reservados con él, la lista de recursos complementarios no contiene datos para ese anuncio de vídeo.

   Para mostrar un anuncio en pantalla independiente, agregue la lógica al script para ejecutar una etiqueta de anuncio en pantalla DFP (DoubleClick for Publishers) normal en la instancia de banner adecuada.

1. Envía la información del titular a una función de la página, normalmente JavaScript, mediante `ExternalInterface`, que muestra los titulares en una ubicación adecuada.

   Esto suele ser un `div`, y la función utiliza el `div ID` para mostrar el titular. Por ejemplo:

   Añada el detector de eventos:

   ```js
   _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
   ```

   Implemente el controlador de escucha:

   ```js
   private function onAdStarted(event:AdPlaybackEvent):void { 
       // check if there are any companion banner 
       if (event.ad && event.ad.companionAssets  
                    && event.ad.companionAssets.length > 0) { 
           for each (var banner:AdBannerAsset in event.ad.companionAssets) { 
               if (ExternalInterface.available) { 
                   //-- call the java script that will handle the banner display. 
                   ExternalInterface.call('addBanner', banner.resourceType,  
                       banner.width, banner.height, banner.bannerData); 
               } 
           } 
       }  
       //...        
   }
   ```

   Ejemplo de JavaScript para gestionar la visualización:

   ```js
   function addBanner(resourceType, width, height, data) { 
       console.log(resourceType + "," +  width + "," +  height); 
   
   //Assume an html element on the page with id like 'banner300x250' 
       var bannerDiv = document.getElementById('banner' + width +  
           'x' + height);  
       if (bannerDiv != null) { 
           if (resourceType == "html") { // for html resource 
               bannerDiv.innerHTML = data; 
           } 
           else if (resourceType == "iframe") { // for iframe resource 
               bannerDiv.innerHTML = "<iframe src='" + data +  
                   "' width='100%' height='100%'></iframe>"; 
           } 
       } 
   }
   ```
