---
description: Video Player Ad-Serving Interface Definition (VPAID) 2.0 proporciona una interfaz común para reproducir anuncios en vídeo. Proporciona una rica experiencia de medios para los usuarios y permite a los editores segmentar mejor los anuncios, rastrear las impresiones de los anuncios y monetizar el contenido de los vídeos.
title: Compatibilidad con anuncios de VPAID 2.0
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '323'
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
* Anuncio VPAID posterior a la emisión

## Cambios en la API {#section_D62F3E059C6C493592D34534B0BFC150}

Se han realizado los siguientes cambios en la API:

* `PTAuditudeMetadata` tiene una  `customAdLoadTimeout` propiedad para cambiar el tiempo de espera predeterminado en el proceso de carga de VPAID.

   El valor de tiempo de espera predeterminado es de 10 segundos.

* `PTMediaPlayerCustomAdNotification` se envía desde la  `PTMediaPlayer` instancia

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

Mientras se reproduce el anuncio de VPAID:

* El anuncio VPAID se muestra en un contenedor de vista sobre la vista del reproductor, por lo que el código que depende de los toques de los usuarios en la vista del reproductor no funciona.
* El reproductor de contenido principal está en pausa y las llamadas a `pause` y `play` en la instancia del reproductor se utilizan para pausar y reanudar el anuncio de VPAID.

* Los anuncios VPAID no tienen una duración predefinida, ya que la publicidad puede ser interactiva.

   Es posible que la duración de la publicidad y la duración total de la pausa publicitaria definidas por la respuesta del servidor de publicidad no sean precisas.

## Implementación de la integración de VPAID 2.0 {#section_63C9C737367C4A0AB4D62E0DC2084141}

Para agregar compatibilidad con VPAID 2.0 en su aplicación iOS:

1. (Opcional) Añada un oyente para eventos de publicidad personalizados.

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerCustomAdNotification:) name:PTMediaPlayerCustomAdNotification object:self.player];
   ```

1. (Opcional) Muestre la notificación.

   ```
   -(void)onMediaPlayerCustomAdNotification:(NSNotification *)notification{    PTCustomAdNotificationObject *notificationObject = [notification.userInfo objectForKey:PTCustomAdNotificationObjectKey];    if (notificationObject)    
   {        NSLog(@"ViewController:: Custom Ad Notification Received: %ld", notificationObject.type);    } 
   
   }
   ```

