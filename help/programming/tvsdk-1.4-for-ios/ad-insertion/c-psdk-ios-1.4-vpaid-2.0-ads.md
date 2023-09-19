---
description: La Definición de la interfaz para servicio de anuncios del reproductor de vídeo (VPAID) 2.0 proporciona una interfaz común para reproducir anuncios de vídeo. Proporciona una experiencia multimedia enriquecida para los usuarios y permite a los editores segmentar mejor los anuncios, rastrear las impresiones de los anuncios y monetizar el contenido de vídeo.
title: Compatibilidad con anuncios VPAID 2.0
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '323'
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
* Anuncio VPAID posterior a la emisión

## Cambios de API {#section_D62F3E059C6C493592D34534B0BFC150}

Se han realizado los siguientes cambios en la API:

* `PTAuditudeMetadata` tiene un `customAdLoadTimeout` para cambiar el tiempo de espera predeterminado en el proceso de carga de VPAID.

  El valor de tiempo de espera predeterminado es 10 segundos.

* `PTMediaPlayerCustomAdNotification` se envía desde el `PTMediaPlayer` instancia

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

Mientras se reproduce el anuncio VPAID:

* El anuncio de VPAID se muestra en un contenedor de vistas encima de la vista del reproductor, por lo que el código que depende de los toques de los usuarios en la vista del reproductor no funciona.
* El reproductor de contenido principal se detiene y llama a `pause` y `play` en la instancia del reproductor se utilizan para pausar y reanudar el anuncio VPAID.

* Los anuncios VPAID no tienen una duración predefinida, ya que el anuncio puede ser interactivo.

  Es posible que la duración del anuncio y la duración total de la pausa publicitaria definidas por la respuesta del servidor de publicidad no sean precisas.

## Implementación de la integración con VPAID 2.0 {#section_63C9C737367C4A0AB4D62E0DC2084141}

Para añadir compatibilidad con VPAID 2.0 en la aplicación de iOS:

1. (Opcional) Agregue un oyente para los eventos de publicidad personalizados.

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerCustomAdNotification:) name:PTMediaPlayerCustomAdNotification object:self.player];
   ```

1. (Opcional) Visualice la notificación.

   ```
   -(void)onMediaPlayerCustomAdNotification:(NSNotification *)notification{    PTCustomAdNotificationObject *notificationObject = [notification.userInfo objectForKey:PTCustomAdNotificationObjectKey];    if (notificationObject)    
   {        NSLog(@"ViewController:: Custom Ad Notification Received: %ld", notificationObject.type);    } 
   
   }
   ```
