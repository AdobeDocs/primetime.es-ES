---
description: Para permitir que funcione la resolución de anuncios, los proveedores de publicidad, como Adobe Primetime y Decisioning, requieren valores de configuración para habilitar la conexión con el proveedor.
title: Metadatos de inserción de publicidad
exl-id: 7245b42c-f3ba-43ec-b895-c1a2d66aa11f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# Información general {#ad-insertion-metadata}

Para permitir que funcione la resolución de anuncios, los proveedores de publicidad, como Adobe Primetime y Decisioning, requieren valores de configuración para habilitar la conexión con el proveedor.

TVSDK incluye la biblioteca de Primetime y Decisioning. Para que el contenido incluya publicidad del servidor de decisiones de publicidad de Primetime, la aplicación debe proporcionar los siguientes datos necesarios `AuditudeSettings` información:

* `mediaID`, que es un identificador único para el vídeo que se va a reproducir.

   El editor asigna el `mediaID` al enviar contenido de vídeo e información de publicidad al servidor de Adobe Primetime ad decisioning. Primetime ad decisioning utiliza este ID para recuperar del servidor información publicitaria relacionada para el vídeo.

* (Opcional) `defaultMediaId`, que especifica los anuncios que se muestran cuando se cumplen las siguientes condiciones:

   * La solicitud al servidor de publicidad no es válida o el contenido está configurado incorrectamente.
   * Primetime y Decisioning están experimentando retrasos en la propagación de los datos.
   * Uno de los procesos back-end de Primetime y Decisioning no funciona correctamente o no está disponible.

   >[!TIP]
   >
   >Adobe recomienda utilizar `defaultMediaId`.

* Su `zoneID`, que se asigna por Adobe, identifica su empresa o sitio web.
* El dominio del servidor de publicidad asignado.
* Otros parámetros de segmentación.

   Puede incluir estos parámetros según sus necesidades y las necesidades del proveedor de publicidad.
