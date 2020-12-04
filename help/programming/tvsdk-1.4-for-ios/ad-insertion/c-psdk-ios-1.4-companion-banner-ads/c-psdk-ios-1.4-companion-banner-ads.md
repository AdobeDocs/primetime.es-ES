---
description: TVSDK es compatible con las publicidades tipo titular complementarias, que son publicidades que acompañan un anuncio lineal y que a menudo permanecen en la página después de que finaliza el anuncio lineal. La aplicación es responsable de mostrar los letreros adjuntos que se proporcionan con un anuncio lineal.
seo-description: TVSDK es compatible con las publicidades tipo titular complementarias, que son publicidades que acompañan un anuncio lineal y que a menudo permanecen en la página después de que finaliza el anuncio lineal. La aplicación es responsable de mostrar los letreros adjuntos que se proporcionan con un anuncio lineal.
seo-title: Publicidades tipo titular complementarias
title: Publicidades tipo titular complementarias
uuid: 6f38f6ec-bc8b-4ea1-845f-90031b3d8a00
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 0%

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

El contenido de un PTAdAsset describe una pancarta adjunta.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

La notificación `PTMediaPlayerAdStartedNotification` devuelve una instancia `PTAd` que contiene una propiedad `companionAssets` (matriz de `PtAdAsset`).
Cada `PtAdAsset` proporciona información sobre cómo mostrar el recurso.

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
     <li id="li_76B945007CE842158B5125422765E0B2">static: Los datos son una dirección URL estática que es una dirección URL directa a una imagen. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> data </td> 
   <td colname="col2"> Los datos del tipo especificado por <span class="codeph"> resourceType</span> para esta pancarta complementaria. </td> 
  </tr> 
 </tbody> 
</table>

## Mostrar publicidades tipo titular {#display-banner-ads}

Para mostrar anuncios en letreros, debe crear instancias de letreros y permitir que TVSDK escuche eventos relacionados con anuncios.

TVSDK proporciona una lista de publicidades tipo titular complementarias que están asociadas con una publicidad lineal a través del evento de notificación `PTMediaPlayerAdPlayStartedNotification`.

Los manifiestos pueden especificar publicidades de titular complementarias mediante:

* Un fragmento de código HTML
* Dirección URL de una página de iFrame
* La dirección URL de una imagen estática o un archivo SWF de Adobe Flash

Para cada anuncio complementario, TVSDK indica los tipos disponibles para la aplicación.

1. Cree una instancia `PTAdBannerView` para cada ranura de publicidad complementaria en la página.

       Asegúrese de que se ha proporcionado la siguiente información:
   
   * Para evitar la recuperación de anuncios complementarios de diferentes tamaños, una instancia de letrero que especifica la anchura y la altura.
   * Tamaños de pancarta estándar.

1. Añada un observador para `PTMediaPlayerAdStartedNotification` que haga lo siguiente:
   1. Borra las publicidades existentes en la instancia del letrero.
   1. Obtiene la lista de publicidades complementarias de `Ad.getCompanionAssets` `PTAd.companionAssets`.
   1. Si la lista de anuncios complementarios no está vacía, repita la lista para las instancias de letreros.

      Cada instancia de pancarta ( a `PTAdAsset`) contiene información como, por ejemplo, ancho, alto, tipo de recurso (html, iframe o static) y datos necesarios para mostrar la pancarta adjunta.
   1. Si una publicidad de vídeo no tiene anuncios complementarios reservados con ella, la lista de recursos complementarios no contiene datos para esa publicidad de vídeo.

      Para mostrar una publicidad en pantalla independiente, agregue la lógica a la secuencia de comandos para ejecutar una etiqueta de visualización de publicidad en DFP normal (DoubleClick para editores) en la instancia de letrero adecuada.
   1. Envía la información del letrero a una función de la página que muestra los letreros en una ubicación adecuada.

      Generalmente es `div` y su función utiliza `div ID` para mostrar la pancarta. Por ejemplo:

      ```
      - (void) onMediaPlayerAdPlayStarted:(NSNotification *) notification { 
          _currentAd  = [notification.userInfo  objectForKey:PTMediaPlayerAdKey];  
          if (_currentAd != nil) { 
              [self removeAllBanners]; // remove any existing PTAdBannerView views 
      
              // banners 
              if (_currentAd.companionAssets && _currentAd.companionAssets.count > 0) { 
                  PTAdAsset *bannerAsset = [_currentAd.companionAssets objectAtIndex:0]; 
      
                  PTAdBannerView *bannerView = [[PTAdBannerView alloc] initWithAsset:bannerAsset];  
                  bannerView.player = self.player; 
                  bannerView.delegate = self; 
      
                  bannerView.frame = CGRectMake(0.0, 0.0, bannerAsset.width, bannerAsset.height);  
                  [_adBannerView.bannerView addSubview:bannerView]; 
              } 
          } 
      }
      ```
