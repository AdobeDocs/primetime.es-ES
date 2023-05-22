---
description: Para mostrar anuncios de banner, debe crear instancias de banner y permitir que TVSDK escuche eventos relacionados con anuncios.
title: Mostrar anuncios de banner
exl-id: 3ccf6525-ffc1-4f45-a662-8b53cab0f448
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 0%

---

# Mostrar anuncios de banner {#display-banner-ads}

Para mostrar anuncios de banner, debe crear instancias de banner y permitir que TVSDK escuche eventos relacionados con anuncios.

TVSDK proporciona una lista de anuncios de banner complementarios asociados a un anuncio lineal a través de `AdPlaybackEventListener.onAdBreakStart` evento.

Los manifiestos pueden especificar anuncios de banner complementarios mediante:

* Un fragmento de HTML
* La dirección URL de una página iFrame
* La URL de una imagen estática o un archivo del SWF del Flash de Adobe

Para cada anuncio complementario, TVSDK indica qué tipos están disponibles para su aplicación.

1. Agregue un oyente para `AdPlaybackEventListener.onAdBreakStart` que hace lo siguiente:

   * Borra los anuncios existentes en la instancia de banner.
   * Obtiene la lista de anuncios complementarios de `Ad.getCompanionAssets`.
   * Si la lista de anuncios complementarios no está vacía, itere en la lista de instancias de banner.

      Cada instancia de banner (un `AdAsset`) contiene información, como anchura, altura, tipo de recurso (html, iframe o estático) y datos necesarios para mostrar el banner complementario.
   * Si un anuncio de vídeo no tiene anuncios complementarios reservados con él, la lista de recursos complementarios no contiene datos para ese anuncio de vídeo.
   * Para mostrar un anuncio en pantalla independiente, agregue la lógica al script para ejecutar una etiqueta de anuncio en pantalla DFP (DoubleClick for Publishers) normal en la instancia de banner adecuada.
   * Envía la información del titular a una función de la página que muestra los titulares en una ubicación adecuada.

      Esto suele ser un `div`, y la función utiliza el `div ID` para mostrar el titular.
