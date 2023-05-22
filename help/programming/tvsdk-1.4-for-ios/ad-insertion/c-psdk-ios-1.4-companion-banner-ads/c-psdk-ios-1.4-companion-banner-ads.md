---
description: TVSDK admite anuncios de banner complementarios, que son anuncios que acompañan a un anuncio lineal y que a menudo permanecen en la página después de que finaliza el anuncio lineal. La aplicación es responsable de mostrar los titulares complementarios que se proporcionan con un anuncio lineal.
title: Anuncios de banner complementarios
exl-id: e7b0ce38-e4b0-4e10-8d76-2d43d8eff665
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '557'
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

El contenido de un PTAdAsset describe un banner complementario.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

El `PTMediaPlayerAdStartedNotification` la notificación devuelve un `PTAd` instancia que contiene un `companionAssets` propiedad (matriz de) `PtAdAsset`).
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
     <li id="li_76B945007CE842158B5125422765E0B2">static: los datos son una URL estática que es una URL directa a una imagen. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> datos </td> 
   <td colname="col2"> Los datos del tipo especificado por. <span class="codeph"> resourceType</span> para este banner complementario. </td> 
  </tr> 
 </tbody> 
</table>

## Mostrar anuncios de banner {#display-banner-ads}

Para mostrar anuncios de banner, debe crear instancias de banner y permitir que TVSDK escuche eventos relacionados con anuncios.

TVSDK proporciona una lista de anuncios de banner complementarios asociados a un anuncio lineal a través de `PTMediaPlayerAdPlayStartedNotification` evento de notificación.

Los manifiestos pueden especificar anuncios de banner complementarios mediante:

* Un fragmento de HTML
* La dirección URL de una página iFrame
* La URL de una imagen estática o un archivo del SWF del Flash de Adobe

Para cada anuncio complementario, TVSDK indica qué tipos están disponibles para su aplicación.

1. Crear un `PTAdBannerView`  para cada espacio publicitario complementario de la página.

       Asegúrese de que se ha proporcionado la siguiente información:
   
   * Para evitar la recuperación de anuncios complementarios de diferentes tamaños, cree una instancia de banner que especifique la anchura y la altura.
   * Tamaños de banner estándar.

1. Añadir un observador para `PTMediaPlayerAdStartedNotification` que hace lo siguiente:
   1. Borra los anuncios existentes en la instancia de banner.
   1. Obtiene la lista de anuncios complementarios de `Ad.getCompanionAssets` `PTAd.companionAssets`.
   1. Si la lista de anuncios complementarios no está vacía, itere en la lista de instancias de banner.

      Cada instancia de banner ( a `PTAdAsset`) contiene información, como anchura, altura, tipo de recurso (html, iframe o estático) y datos necesarios para mostrar el banner complementario.
   1. Si un anuncio de vídeo no tiene anuncios complementarios reservados con él, la lista de recursos complementarios no contiene datos para ese anuncio de vídeo.

      Para mostrar un anuncio en pantalla independiente, agregue la lógica al script para ejecutar una etiqueta de anuncio en pantalla DFP (DoubleClick for Publishers) normal en la instancia de banner adecuada.
   1. Envía la información del titular a una función de la página que muestra los titulares en una ubicación adecuada.

      Esto suele ser un `div`, y la función utiliza el `div ID` para mostrar el titular. Por ejemplo:

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
