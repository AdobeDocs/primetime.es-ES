---
description: La definición de interfaz de servicio de publicidad (VPAID) 2.0 del reproductor de vídeo proporciona una interfaz común para reproducir anuncios en vídeo. Proporciona una experiencia multimedia rica a los usuarios y permite a los editores dirigir mejor los anuncios, rastrear las impresiones de publicidad y monetizar el contenido de vídeo.
seo-description: La definición de interfaz de servicio de publicidad (VPAID) 2.0 del reproductor de vídeo proporciona una interfaz común para reproducir anuncios en vídeo. Proporciona una experiencia multimedia rica a los usuarios y permite a los editores dirigir mejor los anuncios, rastrear las impresiones de publicidad y monetizar el contenido de vídeo.
seo-title: Compatibilidad con anuncios VPAID 2.0
title: Compatibilidad con anuncios VPAID 2.0
uuid: e45e91d2-2aef-4d69-ac80-228d23e8fd7b
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Información general {#vpaid-ad-support-overview}

La definición de interfaz de servicio de publicidad (VPAID) 2.0 del reproductor de vídeo proporciona una interfaz común para reproducir anuncios en vídeo. Proporciona una experiencia multimedia rica a los usuarios y permite a los editores dirigir mejor los anuncios, rastrear las impresiones de publicidad y monetizar el contenido de vídeo.

Se admiten las siguientes funciones:

* Versión 2.0 de la especificación VPAID

   Para obtener más información, consulte [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf).
* Anuncios VPAID lineales con contenido de vídeo a petición (VOD)
* Anuncios VPAID de JavaScript

   Las publicidades VPAID deben estar basadas en JavaScript y la respuesta de publicidad debe identificar el tipo de medio de la publicidad VPAID como `application/javascript`.

No se admiten las siguientes funciones:

* Versión 1.0 de la especificación VPAID
* Anuncios omisibles
* Anuncios no lineales, como anuncios superpuestos, anuncios combinados dinámicos, anuncios minimizables, publicidades contraíbles y anuncios ampliables
* Precarga de publicidades VPAID
* Anuncios VPAID en contenido activo
* Publicidades Flash VPAID

## API

Los siguientes elementos de API admiten anuncios VPAID 2.0:

* El `getCustomAdView` método de `MediaPlayer` devuelve un `CustomAdView` objeto, que representa la vista de web que representa la publicidad VPAID (consulte Referencias [de](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/index.html)API).

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` establece el tiempo de espera en el proceso de carga de VPAID. El valor de tiempo de espera predeterminado es 10 segundos.

Mientras se reproduce la publicidad VPAID:

* La publicidad VPAID se muestra en un contenedor de vistas sobre la vista del reproductor, por lo que el código que depende de los toques de los usuarios en la vista del reproductor no funciona.
* Las llamadas a `pause` y `play` en la instancia del reproductor pausan y reanudan la publicidad VPAID.

* Las publicidades VPAID no tienen una duración predefinida, ya que la publicidad puede ser interactiva.

   Es posible que la duración de la publicidad y la duración total de la pausa publicitaria especificadas en la respuesta del servidor de publicidad no sean precisas.