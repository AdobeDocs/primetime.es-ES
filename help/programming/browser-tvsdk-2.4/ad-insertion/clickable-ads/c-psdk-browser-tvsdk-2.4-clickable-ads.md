---
description: El TVSDK del explorador proporciona a su aplicación de vídeo la información necesaria para responder al clic de un usuario en un anuncio en el que se puede hacer clic.
title: Anuncios en los que se puede hacer clic
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---

# Información general {#clickable-ads-overview}

El TVSDK del explorador proporciona a su aplicación de vídeo la información necesaria para responder al clic de un usuario en un anuncio en el que se puede hacer clic.

Cuando un usuario hace clic en un anuncio en el que se puede hacer clic, una respuesta típica de una aplicación de vídeo es abrir una nueva ventana del explorador y navegar a la dirección URL asociada con el anuncio. Para facilitar esto, el TVSDK del explorador se activa y genera notificaciones que la aplicación puede utilizar para administrar el proceso de pulsación.

En la aplicación, puede proporcionar al usuario un control en el que hacer clic (por ejemplo, un botón) mientras se reproduce el anuncio en el que se puede hacer clic. Debe crear controladores para los eventos activados por el TVSDK del explorador que estén asociados con el anuncio (por ejemplo, inicio del anuncio, clic en y finalización del anuncio). Por último, debe implementar los comportamientos específicos que la aplicación seguirá tras el clic de un usuario en un anuncio (por ejemplo, si debe pausar o no el anuncio, mostrar la URL de pulsación, etc.).

>[!NOTE]
>
>El reproductor de referencia incluido con el TVSDK del explorador incluye una posible solución práctica para procesar anuncios de pulsaciones.
