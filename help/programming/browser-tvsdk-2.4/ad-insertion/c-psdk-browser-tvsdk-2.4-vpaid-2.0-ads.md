---
description: La definición de interfaz de servicio de publicidad (VPAID) 2.0 del reproductor de vídeo proporciona una interfaz común para reproducir anuncios de vídeo. Proporciona una rica experiencia de medios para los usuarios y permite a los editores segmentar mejor los anuncios, rastrear las impresiones de los anuncios y monetizar el contenido de los vídeos.
title: Compatibilidad con anuncios de VPAID 2.0
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Compatibilidad con anuncios de VPAID 2.0 {#vpaid-ad-support}

La definición de interfaz de servicio de publicidad (VPAID) 2.0 del reproductor de vídeo proporciona una interfaz común para reproducir anuncios de vídeo. Proporciona una rica experiencia de medios para los usuarios y permite a los editores segmentar mejor los anuncios, rastrear las impresiones de los anuncios y monetizar el contenido de los vídeos.

Se admiten las siguientes funciones:

* Versión 2.0 de la especificación VPAID

   Para obtener más información, consulte [IAB VPAID 2.0](https://www.iab.com/guidelines/digital-video-player-ad-interface-definition-vpaid-2-0/).
* Anuncios VPAID lineales con contenido de vídeo bajo demanda (VOD)
* En el contenido activo, el TVSDK del explorador admite anuncios VPAID de JavaScript previos a la emisión.
* En el modo de reserva de Flash, el SDK de explorador solo admite anuncios VPAID basados en Flash.
* Anuncios VPAID de JavaScript lineales

   Los anuncios VPAID deben estar basados en JavaScript y la respuesta de anuncio debe identificar el tipo de medio del anuncio VPAID como `application/javascript`.

No se admiten las siguientes funciones:

* Versión 1.0 de la especificación VPAID
* Anuncios omitidos
* Anuncios no lineales, como anuncios superpuestos, anuncios complementarios dinámicos, anuncios minimizables, anuncios contraíbles y anuncios ampliables.
* Precarga de anuncios VPAID
* Anuncios VPAID en contenido en directo
* Flash de anuncios VPAID

## API {#section_0DB1D383CA5047B281BC808BC082C69B}

Los siguientes elementos de API admiten los anuncios VPAID 2.0:

* El método `getCustomAdView` de `MediaPlayer` devuelve un objeto `CustomAdView`, que representa la vista web que renderiza la publicidad VPAID.

   Para obtener más información sobre el método `getCustomAdView`, consulte [Documentación de la API de MediaPlayer](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.MediaPlayer.html).

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` establece el tiempo de espera en el proceso de carga de VPAID.

   El valor de tiempo de espera predeterminado es de 10 segundos.

* La API, `auditudeSettings.ignoreVPAIDAds`, le permite ignorar las publicidades VPAID recibidas del servidor de Auditude. La API no funciona para la reserva de Flash.

Mientras se reproduce el anuncio de VPAID:

* El anuncio VPAID se muestra en un contenedor de vistas sobre la vista del reproductor, por lo que el código que depende de los toques de los usuarios en la vista del reproductor no funciona.
* Llamadas a para pausar y reproducir en la instancia del reproductor para pausar y reanudar el anuncio de VPAID.
* Los anuncios VPAID no tienen una duración predefinida, ya que la publicidad puede ser interactiva.

   Es posible que la duración de la publicidad y la duración total de la pausa publicitaria que se especifican en la respuesta del servidor de publicidad no sean precisas.