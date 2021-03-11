---
description: Cuando el TVSDK del explorador solicita una publicidad que no está en el servidor de publicidad principal, el reproductor debe solicitar la publicidad desde el servidor secundario. La plantilla de servicio de publicidad de vídeo (VAST) establece el estándar de comunicación entre servidores de publicidad y reproductores de vídeo, y es la respuesta que envía el servidor de publicidad secundario cuando solicita el anuncio.
title: Anuncios VAST
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# Anuncios VAST {#vast-ads}

Cuando el TVSDK del explorador solicita una publicidad que no está en el servidor de publicidad principal, el reproductor debe solicitar la publicidad desde el servidor secundario. La plantilla de servicio de publicidad de vídeo (VAST) establece el estándar de comunicación entre servidores de publicidad y reproductores de vídeo, y es la respuesta que envía el servidor de publicidad secundario cuando solicita el anuncio.

Para obtener más información sobre VAST, consulte [Plantilla de servicio de publicidad de vídeo digital (VAST) 3.0](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf).

El SDK de TVSDK del explorador admite los siguientes elementos de publicidad VAST:

## Anuncios envolventes y en línea {#section_11B8A1A8F52F4F77981C6AAC02185087}

Se admiten los siguientes elementos:

* **`wrapper`** Cuando el reproductor necesita ponerse en contacto con un servidor de publicidad secundario para solicitar una publicidad, el elemento wrapper proporciona la información de redirección. Un elemento envolvente puede señalar a varios contenedores que finalmente apuntan a un anuncio VAST.

* **`inline`** Se admiten los siguientes elementos obligatorios:

* `AdSystem`
* `AdTitle`
* `Impression`

   Se admiten los siguientes elementos opcionales:

* `Description`
* `Survey`
* `Error`

## Creativos {#section_0121F948CB074E49A8132D202786CAA4}

Este elemento es un archivo que forma parte de un anuncio VAST y contiene un elemento `creative` que puede admitir un anuncio lineal, un anuncio no lineal o un anuncio complementario. En el elemento `creative`, se admiten los elementos `id`, `sequence` y `adId`.

A continuación se muestra más información sobre los tipos de publicidad:

* **Anuncios** linealesSe admiten los siguientes elementos:

   * `TrackingEvent`, que contiene el  `Tracking` elemento .
      * `Duration`
      * `AdParameters`
      * `VideoClicks`, lo que incluye lo siguiente:

      * `ClickThrough`
      * `ClickTracking`
      * `CustomClick`

      * `MediaFiles`

      * `MediaFile`

         >[!TIP]
         >
         >En este elemento, se admiten los atributos `id`, `bitrate`, `delivery`, `width`, `height`, `scalable`, `maintainAspectRatio`, `apiFramework` y `type`.

* **Anuncios no** linealesSe admiten los siguientes elementos:

   * `Non-linear`

      >[!TIP]
      >
      >En este elemento, se admiten los atributos `id`, `width`, `height`, `apiFramework`, `expandedWidth`, `expandedHeight`, `scalable`, `maintainAspectRatio` y `minSuggestedDuration`.

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `NonLinearClickThrough`
      * `AdParameters`

* **Anuncios** complementariosSe admiten los siguientes elementos:

   * `Companion`

      >[!TIP]
      >
      >En este elemento, se admiten los atributos `id`, `width`, `height`, `apiFramework`, `expandedWidth` y `expandedHeight`.

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `TrackingEvents`

## Extensiones {#section_17401C75F419453BAE83637EEB6E1E60}

>[!TIP]
>
>Solo se admiten extensiones específicas de Auditude.

* `Extension`
