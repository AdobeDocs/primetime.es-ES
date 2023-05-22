---
description: La definición de la interfaz del servidor de anuncios del reproductor de vídeo (VPAID) 2.0 proporciona una interfaz común para reproducir anuncios de vídeo. Proporciona una experiencia multimedia enriquecida para los usuarios y permite a los editores segmentar mejor los anuncios, rastrear las impresiones de los anuncios y monetizar el contenido de vídeo.
title: Compatibilidad con anuncios VPAID 2.0
exl-id: ea3dcd1d-c4e2-46c6-b613-e86c3e161ca8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# Compatibilidad con anuncios VPAID 2.0 {#vpaid-ad-support}

La definición de la interfaz del servidor de anuncios del reproductor de vídeo (VPAID) 2.0 proporciona una interfaz común para reproducir anuncios de vídeo. Proporciona una experiencia multimedia enriquecida para los usuarios y permite a los editores segmentar mejor los anuncios, rastrear las impresiones de los anuncios y monetizar el contenido de vídeo.

Se admiten las siguientes funciones:

* Versión 2.0 de la especificación VPAID

   Para obtener más información, consulte [IAB VPAID 2.0](https://www.iab.com/guidelines/digital-video-player-ad-interface-definition-vpaid-2-0/).
* Anuncios VPAID lineales con contenido de vídeo bajo demanda (VOD)
* En el contenido en directo, el TVSDK del explorador admite anuncios VPAID de JavaScript previos a la emisión.
* En el modo de reserva de Flash, el TVSDK del explorador solo admite anuncios VPAID basados en Flash.
* Anuncios VPAID de JavaScript lineales

   Los anuncios VPAID deben estar basados en JavaScript y la respuesta de publicidad debe identificar el tipo de medio del anuncio VPAID como `application/javascript`.

No se admiten las siguientes funciones:

* Versión 1.0 de la especificación VPAID
* Anuncios omitibles
* Anuncios no lineales, como anuncios de superposición, anuncios compañeros dinámicos, anuncios minimizables, anuncios contraíbles y anuncios expandibles.
* Precarga de anuncios VPAID
* Anuncios VPAID en contenido en directo
* Flash de anuncios VPAID

## API {#section_0DB1D383CA5047B281BC808BC082C69B}

Los siguientes elementos de API admiten anuncios VPAID 2.0:

* El `getCustomAdView` método de `MediaPlayer` devuelve un valor `CustomAdView` , que representa la vista web que procesa el anuncio VPAID.

   Para obtener más información sobre `getCustomAdView` método, consulte [Documentación de API de MediaPlayer](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.MediaPlayer.html).

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` establece el tiempo de espera en el proceso de carga de VPAID.

   El valor de tiempo de espera predeterminado es 10 segundos.

* La API de, `auditudeSettings.ignoreVPAIDAds`, permite ignorar los anuncios VPAID recibidos del servidor de Auditude. La API no funciona para la reserva de Flash.

Mientras se reproduce el anuncio VPAID:

* El anuncio de VPAID se muestra en un contenedor de vistas encima de la vista del reproductor, por lo que el código que depende de los toques de los usuarios en la vista del reproductor no funciona.
* Las llamadas para pausar y reproducir en la instancia del reproductor pausan y reanudan el anuncio de VPAID.
* Los anuncios VPAID no tienen una duración predefinida, ya que el anuncio puede ser interactivo.

   Es posible que la duración de la publicidad y la duración total de la pausa publicitaria especificadas en la respuesta del servidor de publicidad no sean precisas.
