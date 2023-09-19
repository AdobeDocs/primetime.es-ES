---
description: La definición de la interfaz del servidor de anuncios del reproductor de vídeo (VPAID) 2.0 proporciona una interfaz común para reproducir anuncios de vídeo. Proporciona una experiencia multimedia enriquecida para los usuarios y permite a los editores segmentar mejor los anuncios, rastrear las impresiones de los anuncios y monetizar el contenido de vídeo.
title: Compatibilidad con anuncios VPAID 2.0
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Compatibilidad con anuncios VPAID 2.0 {#vpaid-ad-support}

La definición de la interfaz del servidor de anuncios del reproductor de vídeo (VPAID) 2.0 proporciona una interfaz común para reproducir anuncios de vídeo. Proporciona una experiencia multimedia enriquecida para los usuarios y permite a los editores segmentar mejor los anuncios, rastrear las impresiones de los anuncios y monetizar el contenido de vídeo.

Se admiten las siguientes funciones:

* Versión 2.0 de la especificación VPAID

  Para obtener más información, consulte [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf).
* Anuncios VPAID lineales con contenido de vídeo bajo demanda (VOD)
* Anuncios VPAID de JavaScript

  Los anuncios VPAID deben estar basados en JavaScript y la respuesta de publicidad debe identificar el tipo de medio del anuncio VPAID como `application/javascript`.

No se admiten las siguientes funciones:

* Versión 1.0 de la especificación VPAID
* Anuncios omitibles
* Anuncios no lineales, como anuncios de superposición, anuncios compañeros dinámicos, anuncios minimizables, anuncios contraíbles y anuncios expandibles
* Precarga de anuncios VPAID
* Anuncios VPAID en contenido en directo
* Flash de anuncios VPAID

## API

Los siguientes elementos de API admiten anuncios VPAID 2.0:

* El `getCustomAdView` método de `MediaPlayer` devuelve un valor `CustomAdView` , que representa la vista web que procesa el anuncio VPAID (consulte [Referencias de API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/index.html)).

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` establece el tiempo de espera en el proceso de carga de VPAID. El valor de tiempo de espera predeterminado es 10 segundos.

Mientras se reproduce el anuncio VPAID:

* El anuncio de VPAID se muestra en un contenedor de vistas encima de la vista del reproductor, por lo que el código que depende de los toques de los usuarios en la vista del reproductor no funciona.
* Llamadas a `pause` y `play` en la instancia del reproductor, pausa y reanuda el anuncio VPAID.

* Los anuncios VPAID no tienen una duración predefinida, ya que el anuncio puede ser interactivo.

  Es posible que la duración de la publicidad y la duración total de la pausa publicitaria especificadas en la respuesta del servidor de publicidad no sean precisas.
