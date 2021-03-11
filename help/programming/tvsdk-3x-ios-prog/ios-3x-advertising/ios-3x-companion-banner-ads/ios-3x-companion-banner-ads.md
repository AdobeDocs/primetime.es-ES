---
description: TVSDK admite anuncios tipo titular adjuntos, que son anuncios que acompañan un anuncio lineal y que a menudo permanecen en la página después de que finaliza el anuncio lineal. La aplicación es responsable de mostrar los banners adjuntos que se proporcionan con un anuncio lineal.
title: Publicidades tipo titular complementarias
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---


# Anuncios del banner Companion {#companion-banner-ads}

TVSDK admite anuncios tipo titular adjuntos, que son anuncios que acompañan un anuncio lineal y que a menudo permanecen en la página después de que finaliza el anuncio lineal. La aplicación es responsable de mostrar los banners adjuntos que se proporcionan con un anuncio lineal.

Cuando muestre anuncios complementarios, siga estas recomendaciones:

* Intente presentar tantos anuncios de banner de acompañamiento de un anuncio de vídeo como se ajuste al diseño del reproductor.
* Presente un banner complementario solo si tiene una ubicación que coincida exactamente con la altura y anchura especificadas.

   >[!TIP]
   >
   >No cambie el tamaño del banner.

* Presente los banners adjuntos lo antes posible después de que comience el anuncio.
* No superponga el contenedor principal de anuncios/vídeos con banners complementarios.
* Continúe mostrando banners complementarios una vez que finalice el anuncio.

   El estándar es mostrar cada banner complementario hasta que tenga un reemplazo para este banner.

## Datos del banner Companion {#companion-banner-data}

El contenido de un PTAdAsset describe un banner complementario.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

La notificación `PTMediaPlayerAdStartedNotification` devuelve una instancia `PTAd` que contiene una propiedad `companionAssets` (matriz `PtAdAsset`).
Cada `PtAdAsset` proporciona información sobre cómo mostrar el recurso.

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>Información disponible</b></th> 
   <th colname="col2" class="entry"><b>Descripción</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> width </td> 
   <td colname="col2"> Anchura del banner complementario en píxeles. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> height </td> 
   <td colname="col2"> Altura del banner complementario en píxeles. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> tipo de recurso </td> 
   <td colname="col2">El tipo de recurso para este banner complementario: 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html: Los datos están en código HTML. </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe: Los datos son una URL de iframe (src). </li> 
     <li id="li_76B945007CE842158B5125422765E0B2">static: Los datos son una dirección URL estática que es una dirección URL directa a una imagen. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> data </td> 
   <td colname="col2"> Los datos del tipo especificado por <span class="codeph">resourceType</span> para este banner complementario. </td> 
  </tr> 
 </tbody> 
</table>

## Mostrar anuncios de tipo titular {#display-banner-ads}

Para mostrar anuncios de banners, debe crear instancias de banners y permitir que TVSDK escuche eventos relacionados con anuncios.

TVSDK proporciona una lista de anuncios de tipo titular asociados a un anuncio lineal a través del evento de notificación `PTMediaPlayerAdPlayStartedNotification`.

Los manifiestos pueden especificar anuncios de banners complementarios mediante:

* Un fragmento HTML
* La dirección URL de una página de iFrame
* La URL de una imagen estática o un archivo SWF de Flash de Adobe

Para cada anuncio complementario, TVSDK indica qué tipos están disponibles para su aplicación.

1. Cree una instancia `PTAdBannerView` para cada espacio de anuncio complementario de la página.

       Asegúrese de que se ha proporcionado la siguiente información:
   
   * Para evitar la recuperación de anuncios complementarios de diferentes tamaños, una instancia de banner que especifique la anchura y la altura.
   * Tamaños de banner estándar.

1. Agregue un observador para el `PTMediaPlayerAdStartedNotification` que haga lo siguiente:
   1. Borra los anuncios existentes en la instancia del banner.
   1. Obtiene la lista de anuncios complementarios de `Ad.getCompanionAssets` `PTAd.companionAssets`.
   1. Si la lista de anuncios complementarios no está vacía, repita la lista para las instancias de banner.

      Cada instancia de banner ( `PTAdAsset`) contiene información, como ancho, alto, tipo de recurso (html, iframe o static) y datos necesarios para mostrar el banner complementario.
   1. Si una publicidad de vídeo no tiene anuncios complementarios reservados con ella, la lista de recursos complementarios no contiene datos para esa publicidad de vídeo.

      Para mostrar un anuncio en pantalla independiente, agregue la lógica a la secuencia de comandos para ejecutar una etiqueta de publicidad de visualización DFP normal (DoubleClick for Publishers) en la instancia de banner adecuada.
   1. Envía la información del banner a una función de la página que muestra los banners en una ubicación adecuada.

      Normalmente es `div` y su función utiliza el `div ID` para mostrar el banner. Por ejemplo:

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
