---
description: Para mostrar anuncios en letreros, debe crear instancias de letreros y permitir que TVSDK escuche eventos relacionados con anuncios.
seo-description: Para mostrar anuncios en letreros, debe crear instancias de letreros y permitir que TVSDK escuche eventos relacionados con anuncios.
seo-title: Mostrar publicidades tipo titular
title: Mostrar publicidades tipo titular
uuid: 7246dfab-860f-4b55-9554-49738a483406
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---


# Mostrar publicidades tipo titular {#display-banner-ads}

Para mostrar anuncios en letreros, debe crear instancias de letreros y permitir que TVSDK escuche eventos relacionados con anuncios.

TVSDK proporciona una lista de publicidades tipo titular complementarias que están asociadas con una publicidad lineal a través del evento `AdPlaybackEventListener.onAdBreakStart`.

Los manifiestos pueden especificar publicidades de titular complementarias mediante:

* Un fragmento de código HTML
* Dirección URL de una página de iFrame
* La dirección URL de una imagen estática o un archivo SWF de Adobe Flash

Para cada anuncio complementario, TVSDK indica los tipos disponibles para la aplicación.

1. Añada un detector para el evento `AdPlaybackEventListener.onAdBreakStart` que haga lo siguiente:

   * Borra las publicidades existentes en la instancia del letrero.
   * Obtiene la lista de publicidades complementarias de `Ad.getCompanionAssets`.
   * Si la lista de anuncios complementarios no está vacía, repita la lista para las instancias de letreros.

      Cada instancia de pancarta (una `AdAsset`) contiene información como, por ejemplo, ancho, alto, tipo de recurso (html, iframe o static) y datos necesarios para mostrar la pancarta adjunta.
   * Si una publicidad de vídeo no tiene anuncios complementarios reservados con ella, la lista de recursos complementarios no contiene datos para esa publicidad de vídeo.
   * Para mostrar una publicidad en pantalla independiente, agregue la lógica a la secuencia de comandos para ejecutar una etiqueta de visualización de publicidad en DFP normal (DoubleClick para editores) en la instancia de letrero adecuada.
   * Envía la información del letrero a una función de la página que muestra los letreros en una ubicación adecuada.

      Generalmente es `div` y su función utiliza `div ID` para mostrar la pancarta.

