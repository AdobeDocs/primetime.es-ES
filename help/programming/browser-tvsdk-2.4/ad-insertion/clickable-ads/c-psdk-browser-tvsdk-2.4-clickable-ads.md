---
description: El TVSDK del explorador proporciona a la aplicación de vídeo la información necesaria para responder al clic de un usuario en una publicidad en la que se puede hacer clic.
seo-description: El TVSDK del explorador proporciona a la aplicación de vídeo la información necesaria para responder al clic de un usuario en una publicidad en la que se puede hacer clic.
seo-title: Publicidades en las que se puede hacer clic
title: Publicidades en las que se puede hacer clic
uuid: 493c3199-b5ba-4809-86eb-e80f10eb957b
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Información general {#clickable-ads-overview}

El TVSDK del explorador proporciona a la aplicación de vídeo la información necesaria para responder al clic de un usuario en una publicidad en la que se puede hacer clic.

Cuando un usuario hace clic en una publicidad en la que se puede hacer clic, una respuesta típica de una aplicación de vídeo es abrir una nueva ventana del explorador y navegar hasta la dirección URL asociada a la publicidad. Para facilitar esto, el SDK de TVSDK del explorador activa las notificaciones de publicidad que la aplicación puede utilizar para administrar el proceso de pulsaciones.

En la aplicación, puede proporcionar al usuario un control para hacer clic (por ejemplo, un botón) mientras se reproduce la publicidad en la que se puede hacer clic. Debe crear controladores para los eventos activados por el TVSDK del explorador que estén asociados con la publicidad (por ejemplo, inicio de anuncio, clic en publicidad y completado). Por último, debe implementar los comportamientos específicos que su aplicación seguirá cuando un usuario haga clic en la publicidad (por ejemplo, si desea pausar la publicidad, mostrar la URL de pulsación, etc.).

>[!NOTE]
>
>El reproductor de referencia incluido con el SDK de TVSDK del explorador incluye una posible solución de trabajo para procesar publicidades de pulsaciones.