---
description: Para permitir que funcione la resolución de anuncios, los proveedores de anuncios, como Adobe Primetime y la toma de decisiones, requieren valores de configuración para habilitar la conexión con el proveedor.
title: Metadatos de inserción de publicidad
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# Información general {#ad-insertion-metadata-overview}

Para permitir que funcione la resolución de anuncios, los proveedores de anuncios, como Adobe Primetime y la toma de decisiones, requieren valores de configuración para habilitar la conexión con el proveedor.

El SDK de explorador incluye la biblioteca de Adobe Primetime y decisiones. Para que el contenido incluya publicidad del servidor de Adobe Primetime y decisiones, la aplicación debe proporcionar la siguiente información requerida de AudidtudeSettings:

* `mediaID`, que es un identificador único para el vídeo que se reproducirá.

   El editor asigna el mediaID al enviar contenido de vídeo e información de publicidad al servidor de Adobe Primetime ad decisioning. Adobe Primetime utiliza este ID para la toma de decisiones de anuncios con el fin de recuperar información de publicidad relacionada para el vídeo desde el servidor.

* (Opcional) `defaultMediaId`, que especifica las publicidades que se proporcionan cuando se cumplen las siguientes condiciones:

   * La solicitud al servidor de publicidad no es válida o el contenido está configurado incorrectamente.
   * La toma de decisiones de anuncios de Adobe Primetime está experimentando retrasos en la propagación de los datos.
   * Uno de los procesos del back-end de la toma de decisiones de anuncios de Adobe Primetime está funcionando mal o no está disponible.

   >[!TIP]
   >
   >Adobe recomienda utilizar `defaultMediaId`.

* El `zoneID`, que se asigna por Adobe, identifica a su empresa o sitio web.
* Dominio del servidor de publicidad asignado.
* Otros parámetros de segmentación.

   Puede incluir estos parámetros en función de sus necesidades y las necesidades del proveedor de publicidad.