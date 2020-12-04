---
description: La definición de interfaz de servicio de publicidad (VPAID) 2.0 del reproductor de vídeo proporciona una interfaz común para reproducir anuncios en vídeo. Proporciona una experiencia multimedia rica a los usuarios y permite a los editores mejorar el destinatario de los anuncios, realizar un seguimiento de las impresiones de los anuncios y monetizar el contenido de los vídeos.
seo-description: La definición de interfaz de servicio de publicidad (VPAID) 2.0 del reproductor de vídeo proporciona una interfaz común para reproducir anuncios en vídeo. Proporciona una experiencia multimedia rica a los usuarios y permite a los editores mejorar el destinatario de los anuncios, realizar un seguimiento de las impresiones de los anuncios y monetizar el contenido de los vídeos.
seo-title: Compatibilidad con anuncios VPAID 2.0
title: Compatibilidad con anuncios VPAID 2.0
uuid: 462692b5-c4b3-4488-adb3-f309809d64ad
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---


# Compatibilidad con anuncios VPAID 2.0 {#vpaid-ad-support}

La definición de interfaz de servicio de publicidad (VPAID) 2.0 del reproductor de vídeo proporciona una interfaz común para reproducir anuncios en vídeo. Proporciona una experiencia multimedia rica a los usuarios y permite a los editores mejorar el destinatario de los anuncios, realizar un seguimiento de las impresiones de los anuncios y monetizar el contenido de los vídeos.

Se admiten las siguientes funciones:

* Versión 2.0 de la especificación VPAID

   Para obtener más información, consulte [IAB VPAID 2.0](https://www.iab.com/guidelines/digital-video-player-ad-interface-definition-vpaid-2-0/).
* Anuncios VPAID lineales con contenido de vídeo a petición (VOD)
* En el contenido en directo, el TVSDK del explorador admite anuncios VPAID de JavaScript anteriores.
* En el modo de reserva de Flash, el SDK de explorador solo admite anuncios VPAID basados en Flash.
* Publicidades VPAID de JavaScript lineales

   Las publicidades VPAID deben estar basadas en JavaScript y la respuesta de publicidad debe identificar el tipo de medio de la publicidad VPAID como `application/javascript`.

No se admiten las siguientes funciones:

* Versión 1.0 de la especificación VPAID
* Anuncios omisibles
* Publicidades no lineales, como anuncios superpuestos, anuncios complementarios dinámicos, anuncios minimizables, publicidades contraíbles y anuncios ampliables.
* Precarga de publicidades VPAID
* Anuncios VPAID en contenido activo
* Publicidades VPAID de Flash

## API {#section_0DB1D383CA5047B281BC808BC082C69B}

Los siguientes elementos de API admiten anuncios VPAID 2.0:

* El método `getCustomAdView` de `MediaPlayer` devuelve un objeto `CustomAdView`, que representa la vista Web que procesa la publicidad VPAID.

   Para obtener más información sobre el método `getCustomAdView`, consulte [documentación de la API de MediaPlayer](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.MediaPlayer.html).

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` establece el tiempo de espera en el proceso de carga de VPAID.

   El valor de tiempo de espera predeterminado es 10 segundos.

* La API, `auditudeSettings.ignoreVPAIDAds`, permite ignorar las publicidades VPAID recibidas del servidor de Auditude. La API no funciona para Flash Fallback.

Mientras se reproduce la publicidad VPAID:

* La publicidad VPAID se muestra en un contenedor de vista sobre la vista del reproductor, por lo que el código que depende de los toques de los usuarios en la vista del reproductor no funciona.
* Las llamadas para pausar y reproducir en la instancia del reproductor pausan y reanudan la publicidad VPAID.
* Las publicidades VPAID no tienen una duración predefinida, ya que la publicidad puede ser interactiva.

   Es posible que la duración de la publicidad y la duración total de la pausa publicitaria especificadas en la respuesta del servidor de publicidad no sean precisas.