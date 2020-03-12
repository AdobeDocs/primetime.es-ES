---
description: TVSDK es compatible con las publicidades tipo titular complementarias, que son publicidades que acompañan un anuncio lineal y que a menudo permanecen en la página después de que finaliza el anuncio lineal. La aplicación es responsable de mostrar los letreros adjuntos que se proporcionan con un anuncio lineal.
seo-description: TVSDK es compatible con las publicidades tipo titular complementarias, que son publicidades que acompañan un anuncio lineal y que a menudo permanecen en la página después de que finaliza el anuncio lineal. La aplicación es responsable de mostrar los letreros adjuntos que se proporcionan con un anuncio lineal.
seo-title: Publicidades tipo titular complementarias
title: Publicidades tipo titular complementarias
uuid: 388a1683-342c-4f3b-97c8-cfcb6c5cfee1
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# Publicidades tipo titular complementarias {#companion-banner-ads}

TVSDK es compatible con las publicidades tipo titular complementarias, que son publicidades que acompañan un anuncio lineal y que a menudo permanecen en la página después de que finaliza el anuncio lineal. La aplicación es responsable de mostrar los letreros adjuntos que se proporcionan con un anuncio lineal.

Al mostrar publicidades complementarias, siga estas recomendaciones:

* Intente presentar tantos anuncios de letreros adjuntos de un anuncio de vídeo como se adapten al diseño del reproductor.
* Presente una pancarta complementaria solo si tiene una ubicación que coincida exactamente con la altura y la anchura especificadas.

   >[!TIP]
   >
   >No cambie el tamaño del letrero.

* Presente los letreros adjuntos lo antes posible después de que comience el anuncio.
* No superponga el contenedor principal de anuncios/vídeos con pancartas complementarias.
* Continúe mostrando las pancartas complementarias una vez que finalice la publicidad.

   El estándar es mostrar cada pancarta adjunta hasta que tenga un reemplazo para esta pancarta.

## Datos de pancarta complementarios {#companion-banner-data}

El contenido de un AdBannerAsset describe una pancarta adjunta.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

El `AdPlaybackEvent.AD_STARTED` evento devuelve una `Ad` instancia que contiene una `companionAssets` propiedad ( `Vector.<AdAsset>`).
Cada uno `AdAsset` proporciona información sobre cómo mostrar el recurso.

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Información disponible </th> 
   <th colname="col2" class="entry"> Descripción </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> width </td> 
   <td colname="col2"> Anchura de la pancarta adjunta en píxeles. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> height </td> 
   <td colname="col2"> Altura del letrero acompañante en píxeles. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> tipo de recurso </td> 
   <td colname="col2">El tipo de recurso para esta pancarta complementaria: 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html: Los datos están en código HTML. </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe: Los datos son una dirección URL de iframe (src). </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> datos de pancarta </td> 
   <td colname="col2"> Datos del tipo especificado por <span class="codeph"> resourceType</span> para este letrero complementario. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> dirección URL estática </td> 
   <td colname="col2"> <p>A veces, el letrero acompañante también tiene una dirección URL estática que es una dirección URL directa a la imagen o a un <span class="filepath"> .swf</span> (letrero flash). </p> <p>Si no desea utilizar html o iframe, puede utilizar una URL directa a una imagen o swf para mostrar el letrero en el escenario Flash. En este caso, puede utilizar staticURL para mostrar la pancarta. </p> <p>Importante:  Debe comprobar si la dirección URL estática es una cadena válida, ya que es posible que esta propiedad no siempre esté disponible. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Mostrar publicidades tipo titular {#display-banner-ads}

Para mostrar anuncios en letreros, debe crear instancias de letreros y permitir que TVSDK escuche eventos relacionados con anuncios.

TVSDK proporciona una lista de publicidades tipo titular complementarias que están asociadas con una publicidad lineal a través del evento de `AdPlaybackEvent.AD_STARTED` evento.

Los manifiestos pueden especificar publicidades de titular complementarias mediante:

* Un fragmento de código HTML
* Dirección URL de una página de iFrame
* La dirección URL de una imagen estática o un archivo SWF de Adobe Flash

Para cada anuncio complementario, TVSDK indica los tipos disponibles para la aplicación.

Agregue un detector para el `AdPlaybackEvent.AD_STARTED` evento que haga lo siguiente:

1. Borra las publicidades existentes en la instancia del letrero.

1. Obtiene la lista de publicidades complementarias de `Ad.companionAssets`.

1. Si la lista de anuncios complementarios no está vacía, repita la lista para las instancias de letrero.

   Cada instancia de pancarta ( una `AdBannerAsset`) contiene información, como ancho, alto, tipo de recurso (html, iframe o static) y datos necesarios para mostrar la pancarta adjunta.

1. Si una publicidad de vídeo no tiene anuncios complementarios reservados con ella, la lista de recursos complementarios no contiene datos para esa publicidad de vídeo.

   Para mostrar una publicidad en pantalla independiente, agregue la lógica a la secuencia de comandos para ejecutar una etiqueta de visualización de publicidad en DFP normal (DoubleClick para editores) en la instancia de letrero adecuada.

1. Envía la información de la pancarta a una función de la página, generalmente JavaScript, mediante `ExternalInterface`la cual se muestran los letreros en una ubicación adecuada.

   Generalmente es un `div`usuario y su función utiliza el `div ID` para mostrar el letrero. Por ejemplo:

   Agregue el detector de eventos:

   ```js
   _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
   ```

   Implementar el controlador de oyentes:

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

   Ejemplo de JavaScript para controlar la visualización:

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
