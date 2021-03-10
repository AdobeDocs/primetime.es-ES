---
description: La definición de la interfaz de servicio de publicidad del reproductor de vídeo (VPAID) proporciona una interfaz común para reproducir anuncios en vídeo. VPAID ofrece una experiencia multimedia completa para los usuarios y permite a los editores segmentar mejor los anuncios, rastrear las impresiones de los anuncios y monetizar el contenido de los vídeos.
title: Requisitos de publicidad personalizados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Requisitos de publicidad personalizados {#custom-ad-requirements}

El reproductor TVSDK puede reproducir anuncios de definición de interfaz de anuncio (VPAID) del reproductor de vídeo digital y mostrar el estado de carga de la publicidad. Si hay errores en el anuncio o los anuncios tardan demasiado en cargarse, TVSDK ignora estos anuncios.

La definición de la interfaz de servicio de publicidad del reproductor de vídeo (VPAID) proporciona una interfaz común para reproducir anuncios en vídeo. VPAID ofrece una experiencia multimedia completa para los usuarios y permite a los editores segmentar mejor los anuncios, rastrear las impresiones de los anuncios y monetizar el contenido de los vídeos.

<!--<a id="section_9A358902CBC24999BA34206EE2029616"></a>-->

El TVSDK admite las siguientes funciones:

* Versión 1.0 y 2.0 de la especificación VPAID
* Anuncios VPAID lineales en contenido de vídeo bajo demanda (VOD)
* Flash de anuncios VPAID

   Los anuncios VPAID deben estar basados en Flashes y la respuesta de anuncio debe identificar el tipo de medio del anuncio VPAID como `application/x-shockwave-flash`.

No se admiten las siguientes funciones:

* Anuncios no lineales, como anuncios superpuestos y anuncios complementarios dinámicos
* Precarga de anuncios VPAID
* Anuncios VPAID en contenido en directo
* Anuncios VPAID de JavaScript

## Estado de carga {#section_5F55C0101CD44A65BCFE1D124CBDF239}

El TVSDK distribuye los siguientes eventos:

* `AdLoading`
* `AdLoaded`
* `AdStarted`
* `AdPlaying`
* `AdStopped`

Después del evento `AdStopped`, el TVSDK reanuda el contenido del vídeo.

>[!TIP]
>
>Si especifica un valor de cero, TVSDK intenta cargar la publicidad hasta que se cargue o hasta que se produzca un error.

## Ignorando anuncios {#section_3EA452F420884335AE90DF23C17E416A}

Si el anuncio tarda demasiado en cargarse o hay errores en el anuncio, el TVSDK puede ignorar el anuncio y el siguiente anuncio del pod de anuncios se reproduce automáticamente.

Si la configuración `AuditudeSettings.customAdLoadTimeout` especifica un número de segundos buenos a cero, el TVSDK intenta cargar la publicidad durante el tiempo especificado. Si no puede cargar la publicidad, esta se omite. Por ejemplo, si configura `AuditudeSettings.customAdLoadTimeout:5`, el TVSDK intenta cargar la publicidad durante un máximo de 5 segundos. Si el anuncio sigue sin cargarse, se ignora.
