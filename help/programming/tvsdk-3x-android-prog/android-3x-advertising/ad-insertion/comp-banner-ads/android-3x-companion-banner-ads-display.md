---
description: Para mostrar anuncios de banners, debe crear instancias de banners y permitir que TVSDK escuche eventos relacionados con anuncios.
title: Mostrar anuncios de tipo titular
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---


# Mostrar anuncios de tipo titular {#display-banner-ads}

Para mostrar anuncios de banners, debe crear instancias de banners y permitir que TVSDK escuche eventos relacionados con anuncios.

TVSDK proporciona una lista de anuncios de tipo titular asociados a un anuncio lineal a través del evento `AdPlaybackEventListener.onAdBreakStart` .

Los manifiestos pueden especificar anuncios de banners complementarios mediante:

* Un fragmento HTML
* La dirección URL de una página de iFrame
* La URL de una imagen estática o un archivo SWF de Flash de Adobe

Para cada anuncio complementario, TVSDK indica qué tipos están disponibles para su aplicación.

1. Añada un oyente para el evento `AdPlaybackEventListener.onAdBreakStart` que haga lo siguiente:

   * Borra los anuncios existentes en la instancia del banner.
   * Obtiene la lista de anuncios complementarios de `Ad.getCompanionAssets`.
   * Si la lista de anuncios complementarios no está vacía, repita la lista para las instancias de banner.

      Cada instancia de banner (un `AdAsset`) contiene información, como ancho, alto, tipo de recurso (html, iframe o static) y datos necesarios para mostrar el banner complementario.
   * Si una publicidad de vídeo no tiene anuncios complementarios reservados con ella, la lista de recursos complementarios no contiene datos para esa publicidad de vídeo.
   * Para mostrar un anuncio en pantalla independiente, agregue la lógica a la secuencia de comandos para ejecutar una etiqueta de publicidad de visualización DFP normal (DoubleClick for Publishers) en la instancia de banner adecuada.
   * Envía la información del banner a una función de la página que muestra los banners en una ubicación adecuada.

      Normalmente es `div` y su función utiliza el `div ID` para mostrar el banner.