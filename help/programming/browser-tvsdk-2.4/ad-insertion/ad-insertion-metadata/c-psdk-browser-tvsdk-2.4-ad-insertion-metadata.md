---
description: Para permitir que funcione la resolución de anuncios, los proveedores de publicidad, como Adobe Primetime y decisiones, requieren valores de configuración para habilitar la conexión con el proveedor.
seo-description: Para permitir que funcione la resolución de anuncios, los proveedores de publicidad, como Adobe Primetime y decisiones, requieren valores de configuración para habilitar la conexión con el proveedor.
seo-title: Metadatos de inserción de anuncio
title: Metadatos de inserción de anuncio
uuid: 8848c939-1f12-4145-8025-453b4fe79aae
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Información general {#ad-insertion-metadata-overview}

Para permitir que funcione la resolución de anuncios, los proveedores de publicidad, como Adobe Primetime y decisiones, requieren valores de configuración para habilitar la conexión con el proveedor.

El SDK de explorador incluye la biblioteca de decisiones y Primetime de Adobe. Para que el contenido incluya publicidad del servidor de decisiones de anuncios de Adobe Primetime, la aplicación debe proporcionar la siguiente información necesaria de AudidtudeSettings:

* `mediaID`, que es un identificador único para el vídeo que se va a reproducir.

   El editor asigna mediaID al enviar contenido de vídeo e información de publicidad al servidor de decisiones de anuncios de Adobe Primetime. Este ID lo utiliza Adobe Primetime y la toma de decisiones de publicidad para recuperar información de publicidad relacionada para el vídeo desde el servidor.

* (Opcional) `defaultMediaId`, que especifica las publicidades que se proporcionan cuando se cumplen las siguientes condiciones:

   * Su solicitud al servidor de publicidad no es válida o el contenido está configurado incorrectamente.
   * La toma de decisiones de publicidad de Adobe Primetime está experimentando retrasos en la propagación de los datos.
   * Uno de los procesos del back-end de Adobe Primetime y de toma de decisiones no funciona correctamente o no está disponible.
   >[!TIP]
   >
   >Adobe recomienda usar `defaultMediaId`.

* El `zoneID`, que es asignado por Adobe, identifica su empresa o sitio web.
* Dominio del servidor de publicidad asignado.
* Otros parámetros de objetivo.

   Puede incluir estos parámetros en función de sus necesidades y las necesidades del proveedor de publicidad.