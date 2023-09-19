---
description: La definición de la interfaz de servicio de anuncios del reproductor de vídeo (VPAID) proporciona una interfaz común para reproducir anuncios de vídeo. VPAID ofrece una experiencia multimedia enriquecida para los usuarios y permite a los editores segmentar mejor los anuncios, rastrear las impresiones de los anuncios y monetizar el contenido de vídeo.
title: Requisitos de publicidad personalizados
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Requisitos de publicidad personalizados {#custom-ad-requirements}

El reproductor TVSDK puede reproducir anuncios de Definición de interfaz de anuncios de reproductor de vídeo digital (VPAID) y mostrar el estado de carga del anuncio. Si hay errores en el anuncio o los anuncios tardan demasiado en cargarse, TVSDK ignora estos anuncios.

La definición de la interfaz de servicio de anuncios del reproductor de vídeo (VPAID) proporciona una interfaz común para reproducir anuncios de vídeo. VPAID ofrece una experiencia multimedia enriquecida para los usuarios y permite a los editores segmentar mejor los anuncios, rastrear las impresiones de los anuncios y monetizar el contenido de vídeo.

<!--<a id="section_9A358902CBC24999BA34206EE2029616"></a>-->

TVSDK admite las siguientes funciones:

* Versiones 1.0 y 2.0 de la especificación VPAID
* Anuncios VPAID lineales en contenido de vídeo bajo demanda (VOD)
* Flash de anuncios VPAID

  Los anuncios VPAID deben basarse en el Flash y la respuesta de publicidad debe identificar el tipo de medio del anuncio VPAID como `application/x-shockwave-flash`.

No se admiten las siguientes funciones:

* Anuncios no lineales como anuncios de superposición y anuncios dinámicos complementarios
* Precarga de anuncios VPAID
* Anuncios VPAID en contenido en directo
* Anuncios VPAID de JavaScript

## Cargando estado {#section_5F55C0101CD44A65BCFE1D124CBDF239}

TVSDK distribuye los siguientes eventos:

* `AdLoading`
* `AdLoaded`
* `AdStarted`
* `AdPlaying`
* `AdStopped`

Después del `AdStopped` evento, TVSDK reanuda el contenido de vídeo.

>[!TIP]
>
>Si especifica un valor de cero, TVSDK intenta cargar el anuncio hasta que se cargue o hasta que se produzca un error.

## Ignorar anuncios {#section_3EA452F420884335AE90DF23C17E416A}

Si el anuncio tarda demasiado en cargarse o hay errores en él, TVSDK puede ignorarlo y el siguiente anuncio del pod de anuncios se reproduce automáticamente.

Si la variable `AuditudeSettings.customAdLoadTimeout` La configuración especifica un número de segundos mayor que cero, el TVSDK intenta cargar el anuncio durante el tiempo especificado. Si no puede cargar el anuncio, este se omitirá. Por ejemplo, si configura `AuditudeSettings.customAdLoadTimeout:5`, el TVSDK intenta cargar el anuncio durante un máximo de 5 segundos. Si el anuncio sigue sin cargarse, se ignora.
