---
description: El SDK de explorador proporciona a la aplicación de vídeo la información necesaria para responder al clic de un usuario en un anuncio en el que se puede hacer clic.
title: Anuncios en los que se puede hacer clic
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# Información general {#clickable-ads-overview}

El SDK de explorador proporciona a la aplicación de vídeo la información necesaria para responder al clic de un usuario en un anuncio en el que se puede hacer clic.

Cuando un usuario hace clic en un anuncio en el que se puede hacer clic, una respuesta habitual de una aplicación de vídeo es abrir una nueva ventana del explorador y navegar a la URL asociada a la publicidad. Para facilitarle este proceso, el SDK de TVSDK del explorador activa y notifica que la aplicación puede utilizar para administrar el proceso de pulsaciones.

En la aplicación, puede proporcionar al usuario un control para hacer clic (por ejemplo, un botón) mientras se reproduce el anuncio en el que se puede hacer clic. Debe crear controladores para los eventos activados por el TVSDK del explorador que estén asociados al anuncio (por ejemplo, inicio de anuncio, publicidad pulsada y finalización). Por último, debe implementar los comportamientos específicos que su aplicación seguirá cuando un usuario haga clic en el anuncio (por ejemplo, para pausar o no la publicidad, mostrar la URL de pulsación, etc.).

>[!NOTE]
>
>El reproductor de referencia incluido con el SDK de TVSDK del explorador incluye una posible solución de trabajo para procesar anuncios en los que se hacen clic.