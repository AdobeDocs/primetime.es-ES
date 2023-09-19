---
description: Para permitir que funcione la resolución de anuncios, los proveedores de publicidad, como Adobe Primetime y Decisioning, requieren valores de configuración para habilitar la conexión con el proveedor.
title: Metadatos de inserción de publicidad
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Información general {#ad-insertion-metadata-overview}

Para permitir que funcione la resolución de anuncios, los proveedores de publicidad, como Adobe Primetime y Decisioning, requieren valores de configuración para habilitar la conexión con el proveedor.

El TVSDK del explorador incluye la biblioteca de Adobe Primetime y Decisioning. Para que el contenido incluya publicidad del servidor de Adobe Primetime ad Decisioning, la aplicación debe proporcionar la siguiente información requerida de AudienceSettings:

* `mediaID`, que es un identificador único para el vídeo que se va a reproducir.

  El publicador asigna el ID de medios al enviar contenido de vídeo e información de publicidad al servidor de Adobe Primetime ad Decisioning. Adobe Primetime ad Decisioning utiliza este ID para recuperar del servidor información publicitaria relacionada para el vídeo.

* (Opcional) `defaultMediaId`, que especifica los anuncios que se muestran cuando se cumplen las siguientes condiciones:

   * La solicitud al servidor de publicidad no es válida o el contenido está configurado incorrectamente.
   * Adobe Primetime Ad Decisioning está experimentando retrasos en la propagación de los datos.
   * Uno de los procesos back-end de Adobe Primetime y Decisioning no funciona correctamente o no está disponible.

  >[!TIP]
  >
  >Adobe recomienda utilizar `defaultMediaId`.

* Su `zoneID`, que se asigna por Adobe, identifica su empresa o sitio web.
* El dominio del servidor de publicidad asignado.
* Otros parámetros de segmentación.

  Puede incluir estos parámetros según sus necesidades y las necesidades del proveedor de publicidad.
