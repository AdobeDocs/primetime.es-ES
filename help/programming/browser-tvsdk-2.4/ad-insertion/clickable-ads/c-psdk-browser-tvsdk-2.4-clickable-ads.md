---
description: El TVSDK del explorador proporciona a su aplicación de vídeo la información necesaria para responder al clic de un usuario en un anuncio en el que se puede hacer clic.
title: Anuncios en los que se puede hacer clic
exl-id: 5fd8b38d-bde7-4d80-bfb0-3390c8f2665c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
