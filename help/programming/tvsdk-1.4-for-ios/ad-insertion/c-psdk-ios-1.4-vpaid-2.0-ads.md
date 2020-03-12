---
description: Video Player Ad-Serving Interface Definition (VPAID) 2.0 proporciona una interfaz común para reproducir anuncios en vídeo. Proporciona una experiencia multimedia rica a los usuarios y permite a los editores dirigir mejor los anuncios, rastrear las impresiones de publicidad y monetizar el contenido de vídeo.
seo-description: Video Player Ad-Serving Interface Definition (VPAID) 2.0 proporciona una interfaz común para reproducir anuncios en vídeo. Proporciona una experiencia multimedia rica a los usuarios y permite a los editores dirigir mejor los anuncios, rastrear las impresiones de publicidad y monetizar el contenido de vídeo.
seo-title: Compatibilidad con anuncios VPAID 2.0
title: Compatibilidad con anuncios VPAID 2.0
uuid: d9a06f3c-0ac2-48aa-b6d2-915184027a38
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Compatibilidad con anuncios VPAID 2.0 {#vpaid-ad-support}

Video Player Ad-Serving Interface Definition (VPAID) 2.0 proporciona una interfaz común para reproducir anuncios en vídeo. Proporciona una experiencia multimedia rica a los usuarios y permite a los editores dirigir mejor los anuncios, rastrear las impresiones de publicidad y monetizar el contenido de vídeo.

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
* Publicidades Flash VPAID
* Publicidad VPAID posterior al lanzamiento

## Cambios en la API {#section_D62F3E059C6C493592D34534B0BFC150}

Se han realizado los siguientes cambios en la API:

* `PTAuditudeMetadata` tiene una `customAdLoadTimeout` propiedad para cambiar el tiempo de espera predeterminado en el proceso de carga de VPAID.

   El valor de tiempo de espera predeterminado es 10 segundos.

* `PTMediaPlayerCustomAdNotification` se envía desde la `PTMediaPlayer` instancia

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

Mientras se reproduce la publicidad VPAID:

* La publicidad VPAID se muestra en un contenedor de vistas sobre la vista del reproductor, de modo que el código que depende de los toques de los usuarios en la vista del reproductor no funciona.
* El reproductor de contenido principal está en pausa y las llamadas a `pause` y `play` en la instancia del reproductor se utilizan para pausar y reanudar la publicidad VPAID.

* Las publicidades VPAID no tienen una duración predefinida, ya que la publicidad puede ser interactiva.

   Es posible que la duración de la publicidad y la duración total de la pausa publicitaria definidas por la respuesta del servidor de publicidad no sean precisas.

## Implementación de la integración con VPAID 2.0 {#section_63C9C737367C4A0AB4D62E0DC2084141}

Para agregar compatibilidad con VPAID 2.0 en la aplicación iOS:

1. (Opcional) Agregue un detector para eventos de publicidad personalizados.

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerCustomAdNotification:) name:PTMediaPlayerCustomAdNotification object:self.player];
   ```

1. (Opcional) Muestre la notificación.

   ```
   -(void)onMediaPlayerCustomAdNotification:(NSNotification *)notification{    PTCustomAdNotificationObject *notificationObject = [notification.userInfo objectForKey:PTCustomAdNotificationObjectKey];    if (notificationObject)    
   {        NSLog(@"ViewController:: Custom Ad Notification Received: %ld", notificationObject.type);    } 
   
   }
   ```

