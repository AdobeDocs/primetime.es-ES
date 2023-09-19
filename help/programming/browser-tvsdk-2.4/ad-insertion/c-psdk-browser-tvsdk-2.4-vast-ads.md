---
description: Cuando el TVSDK del explorador solicita un anuncio que no está en el servidor de publicidad principal, el reproductor debe solicitar el anuncio del servidor secundario. La plantilla de servicio de anuncios de vídeo (VAST) establece el estándar de comunicación entre servidores de publicidad y reproductores de vídeo y es la respuesta que envía el servidor de publicidad secundario cuando se solicita el anuncio.
title: Anuncios VAST
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# Anuncios VAST {#vast-ads}

Cuando el TVSDK del explorador solicita un anuncio que no está en el servidor de publicidad principal, el reproductor debe solicitar el anuncio del servidor secundario. La plantilla de servicio de anuncios de vídeo (VAST) establece el estándar de comunicación entre servidores de publicidad y reproductores de vídeo y es la respuesta que envía el servidor de publicidad secundario cuando se solicita el anuncio.

Para obtener más información sobre VAST, consulte [Plantilla de servicio de anuncios de vídeo digital (VAST) 3.0](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf).

El TVSDK del explorador es compatible con los siguientes elementos de publicidad VAST:

## Envoltorio y anuncios en línea {#section_11B8A1A8F52F4F77981C6AAC02185087}

Se admiten los siguientes elementos:

* **`wrapper`** Cuando el reproductor debe ponerse en contacto con un servidor de publicidad secundaria para solicitar una publicidad, el elemento envoltorio proporciona la información de redirección. Un elemento envolvente puede apuntar a varios envoltorios que finalmente apuntan a un anuncio VAST.

* **`inline`** Se admiten los siguientes elementos necesarios:

* `AdSystem`
* `AdTitle`
* `Impression`

  Se admiten los siguientes elementos opcionales:

* `Description`
* `Survey`
* `Error`

## Creativos {#section_0121F948CB074E49A8132D202786CAA4}

Este elemento es un archivo que forma parte de un anuncio VAST y contiene un `creative` que pueden admitir un anuncio lineal, uno no lineal o un anuncio complementario. En el `creative` , el `id`, `sequence`, y `adId` son compatibles.

Aquí tiene más información sobre los tipos de anuncios:

* **Anuncios lineales** Se admiten los siguientes elementos:

   * `TrackingEvent`, que contiene el `Tracking` Elemento.
      * `Duration`
      * `AdParameters`
      * `VideoClicks`, incluidos los siguientes:

      * `ClickThrough`
      * `ClickTracking`
      * `CustomClick`

      * `MediaFiles`

      * `MediaFile`

        >[!TIP]
        >
        >En este elemento, la variable `id`, `bitrate`, `delivery`, `width`, `height`, `scalable`, `maintainAspectRatio`, `apiFramework`, y `type` se admiten atributos de.

* **Anuncios no lineales** Se admiten los siguientes elementos:

   * `Non-linear`

     >[!TIP]
     >
     >En este elemento, la variable `id`, `width`, `height`, `apiFramework`, `expandedWidth`, `expandedHeight`, `scalable`, `maintainAspectRatio`, y `minSuggestedDuration` se admiten atributos de.

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `NonLinearClickThrough`
      * `AdParameters`

* **Anuncios complementarios** Se admiten los siguientes elementos:

   * `Companion`

     >[!TIP]
     >
     >En este elemento, la variable `id`, `width`, `height`, `apiFramework`, `expandedWidth`, y `expandedHeight` se admiten atributos de.

      * `StaticResource`
      * `IFrameResource`
      * `HTMLResource`
      * `TrackingEvents`

## Extensiones {#section_17401C75F419453BAE83637EEB6E1E60}

>[!TIP]
>
>Solo se admiten extensiones específicas del Auditude.

* `Extension`
