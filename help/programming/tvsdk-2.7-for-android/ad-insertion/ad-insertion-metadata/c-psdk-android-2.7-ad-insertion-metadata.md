---
description: Para permitir que funcione la resolución de anuncios, los proveedores de publicidad, como Adobe Primetime y Decisioning, requieren valores de configuración para habilitar la conexión con el proveedor.
title: Metadatos de inserción de publicidad
exl-id: fb78da4c-129e-4ecd-b598-3ab8af40d713
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# Información general {#ad-insertion-metadata-overview}

Para permitir que funcione la resolución de anuncios, los proveedores de publicidad, como Adobe Primetime y Decisioning, requieren valores de configuración para habilitar la conexión con el proveedor.

TVSDK incluye la biblioteca de Primetime y Decisioning. Para que el contenido incluya publicidad desde el servidor de Primetime ad Decisioning, la aplicación debe proporcionar los siguientes datos necesarios `AuditudeSettings` información:

* `mediaID`, que es un identificador único para el vídeo que se va a reproducir.

   El publicador asigna el ID de medios al enviar contenido de vídeo e información de publicidad al servidor de Adobe Primetime ad Decisioning. Primetime ad decisioning utiliza este ID para recuperar del servidor información publicitaria relacionada para el vídeo.

* (Opcional) `defaultMediaId`, que especifica los anuncios que se muestran cuando se cumplen las siguientes condiciones:

   * La solicitud al servidor de publicidad no es válida o el contenido está configurado incorrectamente.
   * Primetime ad Decisioning está experimentando retrasos en la propagación de los datos.
   * Uno de los procesos back-end de Primetime y Decisioning no funciona correctamente o no está disponible.

   >[!TIP]
   >
   >Adobe recomienda utilizar `defaultMediaId`.

* Su `zoneID`, que se asigna por Adobe, identifica su empresa o sitio web.
* El dominio del servidor de publicidad asignado.
* Otros parámetros de segmentación.

   Puede incluir estos parámetros según sus necesidades y las necesidades del proveedor de publicidad.
