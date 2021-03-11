---
description: Para permitir que funcione la resolución de anuncios, los proveedores de anuncios, como Adobe Primetime y la toma de decisiones, requieren valores de configuración para habilitar la conexión con el proveedor.
title: Metadatos de inserción de publicidad
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Información general {#ad-insertion-metadata-overview}

Para permitir que funcione la resolución de anuncios, los proveedores de anuncios, como Adobe Primetime y la toma de decisiones, requieren valores de configuración para habilitar la conexión con el proveedor.

TVSDK incluye la biblioteca de decisiones de anuncios de Primetime. Para que el contenido incluya publicidad del servidor de decisiones de anuncios de Primetime, la aplicación debe proporcionar la siguiente información requerida: `AuditudeSettings`

* `mediaID`, que es un identificador único para el vídeo que se reproducirá.

   El editor asigna el mediaID al enviar contenido de vídeo e información de publicidad al servidor de Adobe Primetime ad decisioning. Primetime ad decisioning utiliza este ID para recuperar información publicitaria relacionada del vídeo del servidor.

* (Opcional) `defaultMediaId`, que especifica las publicidades que se proporcionan cuando se cumplen las siguientes condiciones:

   * La solicitud al servidor de publicidad no es válida o el contenido está configurado incorrectamente.
   * Las decisiones de anuncios de Primetime están experimentando retrasos en la propagación de los datos.
   * Uno de los procesos back-end de Primetime y decisioning está funcionando mal o no está disponible.

   >[!TIP]
   >
   >Adobe recomienda utilizar `defaultMediaId`.

* El `zoneID`, que se asigna por Adobe, identifica a su empresa o sitio web.
* Dominio del servidor de publicidad asignado.
* Otros parámetros de segmentación.

   Puede incluir estos parámetros en función de sus necesidades y las necesidades del proveedor de publicidad.