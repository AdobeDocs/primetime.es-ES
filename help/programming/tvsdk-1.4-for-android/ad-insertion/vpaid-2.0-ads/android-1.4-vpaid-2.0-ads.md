---
description: Video Player Ad-Serving Interface Definition (VPAID) 2.0 proporciona una interfaz común para reproducir anuncios en vídeo. Proporciona una rica experiencia de medios para los usuarios y permite a los editores segmentar mejor los anuncios, rastrear las impresiones de los anuncios y monetizar el contenido de los vídeos.
title: Compatibilidad con anuncios de VPAID 2.0
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---


# Compatibilidad con anuncios de VPAID 2.0 {#vpaid-ad-support}

Video Player Ad-Serving Interface Definition (VPAID) 2.0 proporciona una interfaz común para reproducir anuncios en vídeo. Proporciona una rica experiencia de medios para los usuarios y permite a los editores segmentar mejor los anuncios, rastrear las impresiones de los anuncios y monetizar el contenido de los vídeos.

Se admiten las siguientes funciones:

* Versión 2.0 de la especificación VPAID

   Para obtener más información, consulte [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf).
* Anuncios VPAID lineales en contenido de vídeo bajo demanda (VOD)
* Anuncios VPAID de JavaScript

   Los anuncios VPAID deben estar basados en JavaScript y la respuesta de anuncio debe identificar el tipo de medio del anuncio VPAID como `application/javascript`.

No se admiten las siguientes funciones:

* Versión 1.0 de la especificación VPAID
* Anuncios omitidos
* Anuncios no lineales, como anuncios superpuestos, anuncios complementarios dinámicos, anuncios minimizables, anuncios contraíbles y anuncios ampliables
* Precarga de anuncios VPAID
* Anuncios VPAID en contenido en directo
* Flash de anuncios VPAID

## Cambios en la API {#section_D62F3E059C6C493592D34534B0BFC150}

Se han realizado los siguientes cambios en la API:

* Se ha agregado una función `getCustomAdView` en `MediaPlayer` y devuelve la vista web que renderiza la publicidad VPAID.

   Para obtener más información sobre el objeto `CustomAdView` que devuelve esta función, consulte [Referencias de API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/index.html).

* Se envía un evento `CUSTOM_AD` desde la instancia del reproductor de medios.

   La aplicación puede registrar una llamada de retorno de evento implementando `CustomAdEventListener`.

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` permite cambiar el tiempo de espera predeterminado en el proceso de carga de VPAID.

   El valor de tiempo de espera predeterminado es de 10 segundos.

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

Mientras se reproduce el anuncio de VPAID:

* El anuncio VPAID se muestra en un contenedor de vista sobre la vista del reproductor, por lo que el código que depende de los toques de los usuarios en la vista del reproductor no funciona.
* El reproductor de contenido principal está en pausa y las llamadas a `pause` y `play` en la instancia del reproductor se utilizan para pausar y reanudar el anuncio de VPAID.

* Los anuncios VPAID no tienen una duración predefinida, ya que la publicidad puede ser interactiva.

   Es posible que la duración de la publicidad y la duración total de la pausa publicitaria definidas por la respuesta del servidor de publicidad no sean precisas.

## Implementación de la integración de VPAID 2.0 {#implement-vpaid-integration}

Para agregar compatibilidad con VPAID 2.0, agregue una vista de anuncio personalizada y oyentes adecuados.

Para añadir compatibilidad con VPAID 2.0:

1. Agregue la vista de anuncio personalizada a la interfaz del reproductor.

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. Añada un oyente para eventos de publicidad personalizados.

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```
