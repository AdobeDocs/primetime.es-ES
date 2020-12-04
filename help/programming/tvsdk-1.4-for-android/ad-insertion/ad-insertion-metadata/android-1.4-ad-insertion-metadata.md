---
description: Para permitir que funcione la resolución de publicidad, los proveedores de publicidad, como Adobe Primetime y la toma de decisiones, requieren valores de configuración para habilitar la conexión con el proveedor.
seo-description: Para permitir que funcione la resolución de publicidad, los proveedores de publicidad, como Adobe Primetime y la toma de decisiones, requieren valores de configuración para habilitar la conexión con el proveedor.
seo-title: Metadatos de inserción de anuncio
title: Metadatos de inserción de anuncio
uuid: f40ed53b-eba1-4f70-a29c-90cac51e8a9a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# Información general {#ad-insertion-metadata}

Para permitir que funcione la resolución de publicidad, los proveedores de publicidad, como Adobe Primetime y la toma de decisiones, requieren valores de configuración para habilitar la conexión con el proveedor.

TVSDK incluye la biblioteca de decisiones y Primetime. Para que el contenido incluya publicidad del servidor de primetime y decisiones, la aplicación debe proporcionar la siguiente información requerida `AuditudeSettings`:

* `mediaID`, que es un identificador único para el vídeo que se va a reproducir.

   El editor asigna `mediaID` al enviar contenido de vídeo e información de publicidad al servidor de decisiones de publicidad de Adobe Primetime. Este ID lo utiliza Primetime y la toma de decisiones para recuperar información de publicidad relacionada para el vídeo desde el servidor.

* (Opcional) `defaultMediaId`, que especifica las publicidades que se proporcionan cuando se cumplen las siguientes condiciones:

   * Su solicitud al servidor de publicidad no es válida o el contenido está configurado incorrectamente.
   * Primetime y la toma de decisiones está experimentando retrasos en la propagación de los datos.
   * Uno de los procesos del back-end de Primetime y decisiones no funciona correctamente o no está disponible.

   >[!TIP]
   >
   >Adobe recomienda utilizar `defaultMediaId`.

* Su `zoneID`, que es asignado por Adobe, identifica su compañía o sitio Web.
* Dominio del servidor de publicidad asignado.
* Otros parámetros de objetivo.

   Puede incluir estos parámetros en función de sus necesidades y las necesidades del proveedor de publicidad.