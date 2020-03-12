---
description: Para permitir que funcione la resolución de anuncios, los proveedores de publicidad, como Adobe Primetime y decisiones, requieren valores de configuración para habilitar la conexión con el proveedor.
seo-description: Para permitir que funcione la resolución de anuncios, los proveedores de publicidad, como Adobe Primetime y decisiones, requieren valores de configuración para habilitar la conexión con el proveedor.
seo-title: Metadatos de inserción de anuncio
title: Metadatos de inserción de anuncio
uuid: 676e81b9-4c2b-487e-bc68-74879ca2966b
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Información general {#ad-nsertion-metadata-overview}

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