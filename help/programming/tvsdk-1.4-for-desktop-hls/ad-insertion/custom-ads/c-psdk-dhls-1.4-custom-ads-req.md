---
description: Video Player Ad-Serving Interface Definition (VPAID) proporciona una interfaz común para reproducir anuncios en vídeo. VPAID proporciona una experiencia multimedia rica para los usuarios y permite a los editores mejorar los destinatarios de anuncios, rastrear impresiones de publicidad y monetizar el contenido de vídeo.
seo-description: Video Player Ad-Serving Interface Definition (VPAID) proporciona una interfaz común para reproducir anuncios en vídeo. VPAID proporciona una experiencia multimedia rica para los usuarios y permite a los editores mejorar los destinatarios de anuncios, rastrear impresiones de publicidad y monetizar el contenido de vídeo.
seo-title: Requisitos de publicidad personalizados
title: Requisitos de publicidad personalizados
uuid: 6d4ba87b-ffe5-467d-8ab5-9795928c2f69
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---


# Requisitos de publicidad personalizados {#custom-ad-requirements}

El reproductor de TVSDK puede reproducir anuncios de definición de interfaz de publicidad (VPAID) del reproductor de vídeo digital y mostrar el estado de carga de la publicidad. Si hay errores en la publicidad o ésta tarda demasiado en cargarse, TVSDK ignora estas publicidades.

Video Player Ad-Serving Interface Definition (VPAID) proporciona una interfaz común para reproducir anuncios en vídeo. VPAID proporciona una experiencia multimedia rica para los usuarios y permite a los editores mejorar los destinatarios de anuncios, rastrear impresiones de publicidad y monetizar el contenido de vídeo.

<!--<a id="section_9A358902CBC24999BA34206EE2029616"></a>-->

El TVSDK admite las siguientes funciones:

* Versión 1.0 y 2.0 de la especificación VPAID
* Anuncios VPAID lineales en contenido de vídeo a petición (VOD)
* Publicidades VPAID de Flash

   Las publicidades VPAID deben estar basadas en Flashes y la respuesta de publicidad debe identificar el tipo de medio de la publicidad VPAID como `application/x-shockwave-flash`.

No se admiten las siguientes funciones:

* Publicidades no lineales, como anuncios superpuestos y publicidades complementarias dinámicas
* Precarga de publicidades VPAID
* Anuncios VPAID en contenido activo
* Anuncios VPAID de JavaScript

## Estado de carga {#section_5F55C0101CD44A65BCFE1D124CBDF239}

TVSDK distribuye los siguientes eventos:

* `AdLoading`
* `AdLoaded`
* `AdStarted`
* `AdPlaying`
* `AdStopped`

Después del evento `AdStopped`, el TVSDK reanuda el contenido del vídeo.

>[!TIP]
>
>Si especifica un valor de cero, TVSDK intentará cargar la publicidad hasta que se cargue o se produzca un error.

## Ignorando anuncios {#section_3EA452F420884335AE90DF23C17E416A}

Si la publicidad tarda demasiado en cargarse o hay errores en la publicidad, el TVSDK puede omitir la publicidad y la siguiente publicidad en el pod de publicidad se reproduce automáticamente.

Si la configuración `AuditudeSettings.customAdLoadTimeout` especifica un número de segundos buenos que cero, el TVSDK intenta cargar la publicidad hasta la duración especificada. Si no puede cargar la publicidad, ésta se omite. Por ejemplo: si configura `AuditudeSettings.customAdLoadTimeout:5`, el TVSDK intenta cargar la publicidad durante un máximo de 5 segundos. Si la publicidad aún no se carga, se ignora.
