---
description: La Definición de la interfaz para servicio de anuncios del reproductor de vídeo (VPAID) 2.0 proporciona una interfaz común para reproducir anuncios de vídeo. Proporciona una experiencia multimedia enriquecida para los usuarios y permite a los editores segmentar mejor los anuncios, rastrear las impresiones de los anuncios y monetizar el contenido de vídeo.
title: Compatibilidad con anuncios VPAID 2.0
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# Compatibilidad con anuncios VPAID 2.0 {#vpaid-ad-support}

La Definición de la interfaz para servicio de anuncios del reproductor de vídeo (VPAID) 2.0 proporciona una interfaz común para reproducir anuncios de vídeo. Proporciona una experiencia multimedia enriquecida para los usuarios y permite a los editores segmentar mejor los anuncios, rastrear las impresiones de los anuncios y monetizar el contenido de vídeo.

Se admiten las siguientes funciones:

* Versión 2.0 de la especificación VPAID

  Para obtener más información, consulte [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf).
* Anuncios VPAID lineales en contenido de vídeo bajo demanda (VOD)
* Anuncios VPAID de JavaScript

  Los anuncios VPAID deben estar basados en JavaScript y la respuesta de publicidad debe identificar el tipo de medio del anuncio VPAID como `application/javascript`.

No se admiten las siguientes funciones:

* Versión 1.0 de la especificación VPAID
* Anuncios omitibles
* Anuncios no lineales como anuncios de superposición, anuncios dinámicos complementarios, anuncios minimizables, anuncios contraíbles y anuncios expandibles
* Precarga de anuncios VPAID
* Anuncios VPAID en contenido en directo
* Flash de anuncios VPAID

## Cambios de API {#section_D62F3E059C6C493592D34534B0BFC150}

Se han realizado los siguientes cambios en la API:

* A `getCustomAdView` se ha añadido la función en `MediaPlayer` y devuelve la vista web que procesa el anuncio VPAID.

  Para obtener más información sobre `CustomAdView` objeto devuelto por esta función, consulte [Referencias de API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/index.html).

* A `CUSTOM_AD` El evento se envía desde la instancia del reproductor de contenidos.

  La aplicación puede registrar una llamada de retorno de evento implementando `CustomAdEventListener`.

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` permite cambiar el tiempo de espera predeterminado en el proceso de carga de VPAID.

  El valor de tiempo de espera predeterminado es 10 segundos.

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

Mientras se reproduce el anuncio VPAID:

* El anuncio de VPAID se muestra en un contenedor de vistas encima de la vista del reproductor, por lo que el código que depende de los toques de los usuarios en la vista del reproductor no funciona.
* El reproductor de contenido principal se detiene y llama a `pause` y `play` en la instancia del reproductor se utilizan para pausar y reanudar el anuncio VPAID.

* Los anuncios VPAID no tienen una duración predefinida, ya que el anuncio puede ser interactivo.

  Es posible que la duración del anuncio y la duración total de la pausa publicitaria definidas por la respuesta del servidor de publicidad no sean precisas.

## Implementación de la integración con VPAID 2.0 {#implement-vpaid-integration}

Para añadir compatibilidad con VPAID 2.0, agregue una vista de anuncio personalizada y los oyentes adecuados.

Para agregar compatibilidad con VPAID 2.0:

1. Añada la vista de anuncio personalizada a la interfaz del reproductor.

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. Agregue un oyente para los eventos de publicidad personalizados.

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```
