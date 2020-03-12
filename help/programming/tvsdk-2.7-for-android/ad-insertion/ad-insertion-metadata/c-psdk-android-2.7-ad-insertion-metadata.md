---
description: Para permitir que funcione la resolución de anuncios, los proveedores de publicidad, como Adobe Primetime y decisiones, requieren valores de configuración para habilitar la conexión con el proveedor.
seo-description: Para permitir que funcione la resolución de anuncios, los proveedores de publicidad, como Adobe Primetime y decisiones, requieren valores de configuración para habilitar la conexión con el proveedor.
seo-title: Metadatos de inserción de anuncio
title: Metadatos de inserción de anuncio
uuid: ee4dd8b8-4c41-4f01-be50-60f4c7dc962d
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Información general {#ad-insertion-metadata-overview}

Para permitir que funcione la resolución de anuncios, los proveedores de publicidad, como Adobe Primetime y decisiones, requieren valores de configuración para habilitar la conexión con el proveedor.

TVSDK incluye la biblioteca de decisiones y Primetime. Para que el contenido incluya publicidad desde Primetime ad decisioningserver, la aplicación debe proporcionar la siguiente `AuditudeSettings` información requerida:

* `mediaID`, que es un identificador único para el vídeo que se va a reproducir.

   El editor asigna mediaID al enviar contenido de vídeo e información de publicidad al servidor de decisiones de anuncios de Adobe Primetime. Este ID lo utiliza Primetime para la toma de decisiones de publicidad a fin de recuperar información de publicidad relacionada para el vídeo desde el servidor.

* (Opcional) `defaultMediaId`, que especifica las publicidades que se proporcionan cuando se cumplen las siguientes condiciones:

   * Su solicitud al servidor de publicidad no es válida o el contenido está configurado incorrectamente.
   * La toma de decisiones de anuncios en horario estelar está experimentando retrasos en la propagación de los datos.
   * Uno de los procesos del back-end de Primetime y decisiones no funciona correctamente o no está disponible.
   >[!TIP]
   >
   >Adobe recomienda usar `defaultMediaId`.

* El `zoneID`, que es asignado por Adobe, identifica su empresa o sitio web.
* Dominio del servidor de publicidad asignado.
* Otros parámetros de objetivo.

   Puede incluir estos parámetros en función de sus necesidades y las necesidades del proveedor de publicidad.