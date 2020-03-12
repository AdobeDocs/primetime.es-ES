---
description: Cuando el TVSDK del explorador solicita una publicidad que no se encuentra en el servidor de publicidad principal, el reproductor debe solicitar la publicidad desde el servidor secundario. La plantilla de servicio de publicidad de vídeo (VAST) establece el estándar de comunicación entre los servidores de publicidad y los reproductores de vídeo y es la respuesta que envía el servidor de publicidad secundario cuando se solicita la publicidad.
seo-description: Cuando el TVSDK del explorador solicita una publicidad que no se encuentra en el servidor de publicidad principal, el reproductor debe solicitar la publicidad desde el servidor secundario. La plantilla de servicio de publicidad de vídeo (VAST) establece el estándar de comunicación entre los servidores de publicidad y los reproductores de vídeo y es la respuesta que envía el servidor de publicidad secundario cuando se solicita la publicidad.
seo-title: Anuncios VAST
title: Anuncios VAST
uuid: 052dae0c-2425-456c-aebe-531f68bb5aa8
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Anuncios VAST {#vast-ads}

Cuando el TVSDK del explorador solicita una publicidad que no se encuentra en el servidor de publicidad principal, el reproductor debe solicitar la publicidad desde el servidor secundario. La plantilla de servicio de publicidad de vídeo (VAST) establece el estándar de comunicación entre los servidores de publicidad y los reproductores de vídeo y es la respuesta que envía el servidor de publicidad secundario cuando se solicita la publicidad.

Para obtener más información sobre VAST, consulte Plantilla de servicio de publicidad de vídeo [digital (VAST) 3.0](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf).

El TVSDK del explorador admite los siguientes elementos de publicidad VAST:

## Publicidades envolventes y en línea {#section_11B8A1A8F52F4F77981C6AAC02185087}

Se admiten los siguientes elementos:

* **`wrapper`** Cuando el reproductor necesita comunicarse con un servidor de publicidad secundario para solicitar una publicidad, el elemento envolvente proporciona la información de redirección. Un elemento envolvente puede apuntar a varios contenedores que finalmente apuntan a un anuncio VAST.

* **`inline`** Se admiten los siguientes elementos necesarios:

* `AdSystem`
* `AdTitle`
* `Impression`

   Se admiten los siguientes elementos opcionales:

* `Description`
* `Survey`
* `Error`

## Elementos creativos {#section_0121F948CB074E49A8132D202786CAA4}

Este elemento es un archivo que forma parte de un anuncio VAST y contiene un `creative` elemento que puede admitir un anuncio lineal, un anuncio no lineal o un anuncio complementario. En el `creative` elemento se admiten los elementos `id`, `sequence`y `adId` .

A continuación encontrará más información sobre los tipos de publicidad:

* **Anuncios** lineales Se admiten los siguientes elementos:

   * `TrackingEvent`, que contiene el `Tracking` elemento.
      * `Duration`
      * `AdParameters`
      * `VideoClicks`, incluidos los siguientes:

      * `ClickThrough`
      * `ClickTracking`
      * `CustomClick`

      * `MediaFiles`

      * `MediaFile`
         [!TIP]
En este elemento, se admiten los atributos `id`, `bitrate`, `delivery`, `width`, `height`, `scalable`, `maintainAspectRatio`, `apiFramework`y `type` .

* **Anuncios** no lineales Se admiten los siguientes elementos:

   * `Non-linear`
      [!TIP]
En este elemento, se admiten los atributos `id`, `width`, `height`, `apiFramework`, `expandedWidth`, `expandedHeight`, `scalable`, `maintainAspectRatio`y `minSuggestedDuration` .

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `NonLinearClickThrough`
      * `AdParameters`

* **Anuncios** complementarios Se admiten los siguientes elementos:

   * `Companion`
      [!TIP]
En este elemento, se admiten los atributos `id`, `width`, `height`, `apiFramework`, `expandedWidth`y `expandedHeight` .

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `TrackingEvents`

## Extensiones {#section_17401C75F419453BAE83637EEB6E1E60}

[!TIP]
Solo se admiten extensiones específicas de Auditude.

* `Extension`