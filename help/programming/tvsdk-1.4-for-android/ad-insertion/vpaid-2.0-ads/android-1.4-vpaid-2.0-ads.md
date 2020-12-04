---
description: Video Player Ad-Serving Interface Definition (VPAID) 2.0 proporciona una interfaz común para reproducir anuncios en vídeo. Proporciona una experiencia multimedia rica a los usuarios y permite a los editores mejorar el destinatario de los anuncios, realizar un seguimiento de las impresiones de los anuncios y monetizar el contenido de los vídeos.
seo-description: Video Player Ad-Serving Interface Definition (VPAID) 2.0 proporciona una interfaz común para reproducir anuncios en vídeo. Proporciona una experiencia multimedia rica a los usuarios y permite a los editores mejorar el destinatario de los anuncios, realizar un seguimiento de las impresiones de los anuncios y monetizar el contenido de los vídeos.
seo-title: Compatibilidad con anuncios VPAID 2.0
title: Compatibilidad con anuncios VPAID 2.0
uuid: 7168a6e4-9c5e-4d3a-8710-867cf98e4445
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 0%

---


# Compatibilidad con anuncios VPAID 2.0 {#vpaid-ad-support}

Video Player Ad-Serving Interface Definition (VPAID) 2.0 proporciona una interfaz común para reproducir anuncios en vídeo. Proporciona una experiencia multimedia rica a los usuarios y permite a los editores mejorar el destinatario de los anuncios, realizar un seguimiento de las impresiones de los anuncios y monetizar el contenido de los vídeos.

Se admiten las siguientes funciones:

* Versión 2.0 de la especificación VPAID

   Para obtener más información, consulte [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf).
* Anuncios VPAID lineales en contenido de vídeo a petición (VOD)
* Anuncios VPAID de JavaScript

   Las publicidades VPAID deben estar basadas en JavaScript y la respuesta de publicidad debe identificar el tipo de medio de la publicidad VPAID como `application/javascript`.

No se admiten las siguientes funciones:

* Versión 1.0 de la especificación VPAID
* Anuncios omisibles
* Publicidades no lineales, como anuncios superpuestos, publicidades complementarias dinámicas, publicidades minimizables, publicidades contraíbles y publicidades ampliables
* Precarga de publicidades VPAID
* Anuncios VPAID en contenido activo
* Publicidades VPAID de Flash

## Cambios de API {#section_D62F3E059C6C493592D34534B0BFC150}

Se han realizado los siguientes cambios en la API:

* Se ha agregado una función `getCustomAdView` en `MediaPlayer` y devuelve la vista web que representa la publicidad VPAID.

   Para obtener más información sobre el objeto `CustomAdView` que devuelve esta función, consulte [Referencias de API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/index.html).

* Se distribuye un evento `CUSTOM_AD` desde la instancia del reproductor de medios.

   La aplicación puede registrar una devolución de llamada de evento implementando `CustomAdEventListener`.

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` le permite cambiar el tiempo de espera predeterminado en el proceso de carga de VPAID.

   El valor de tiempo de espera predeterminado es 10 segundos.

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

Mientras se reproduce la publicidad VPAID:

* La publicidad VPAID se muestra en un contenedor de vista sobre la vista del reproductor, de modo que el código que depende de los toques de los usuarios en la vista del reproductor no funciona.
* El reproductor de contenido principal está en pausa y las llamadas a `pause` y `play` en la instancia del reproductor se utilizan para pausar y reanudar la publicidad VPAID.

* Las publicidades VPAID no tienen una duración predefinida, ya que la publicidad puede ser interactiva.

   Es posible que la duración de la publicidad y la duración total de la pausa publicitaria definidas por la respuesta del servidor de publicidad no sean precisas.

## Implementar la integración de VPAID 2.0 {#implement-vpaid-integration}

Para agregar compatibilidad con VPAID 2.0, agregue una vista de publicidad personalizada y los oyentes adecuados.

Para agregar compatibilidad con VPAID 2.0:

1. Añada la vista de publicidad personalizada en la interfaz del reproductor.

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. Añada un oyente para eventos de publicidad personalizados.

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```
