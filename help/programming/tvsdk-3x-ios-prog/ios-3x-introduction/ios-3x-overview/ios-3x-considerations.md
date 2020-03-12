---
description: Para utilizar TVSDK de forma más eficaz, debe tener en cuenta determinados detalles de su funcionamiento y seguir determinadas prácticas recomendadas.
seo-description: Para utilizar TVSDK de forma más eficaz, debe tener en cuenta determinados detalles de su funcionamiento y seguir determinadas prácticas recomendadas.
seo-title: Consideraciones y prácticas recomendadas
title: Consideraciones y prácticas recomendadas
uuid: a65c9739-ed83-4519-8ae5-7ba4c8f1ca49
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Consideraciones y prácticas recomendadas {#considerations-and-best-practices}

Para utilizar TVSDK de forma más eficaz, debe tener en cuenta determinados detalles de su funcionamiento y seguir determinadas prácticas recomendadas.

## Consideraciones {#section_tvsdk_considerations}

Recuerde la siguiente información al utilizar TVSDK:

* Adobe Primetime no funciona en los simuladores de iOS.

   Debe utilizar dispositivos reales para realizar pruebas.

* La reproducción solo es compatible con el contenido de HTTP Live Streaming (HLS).

* El contenido de vídeo principal se puede multiplexar, donde los flujos de vídeo y audio están en la misma representación, o no multiplexados, donde los flujos de audio y vídeo están en representaciones independientes.

* La API de TVSDK se implementa en Objective-C.

* La reproducción de vídeo requiere el marco de trabajo nativo de Apple AV Foundation. Esto afecta a cómo y cuándo se puede acceder a los recursos de medios, incluidos los subtítulos cerrados y las líneas de tiempo:

   * Los ajustes de línea de tiempo no se pueden revisar después de la configuración inicial.

      Por ejemplo, un anuncio no se puede eliminar de la línea de tiempo después de reproducirse. Si el usuario vuelve a buscar en la presentación, el mismo anuncio se reproduce incluso si la política hubiera sido eliminar el anuncio.

   * Según la precisión del codificador, la duración real del medio codificado puede diferir de las duraciones registradas en el manifiesto del recurso de flujo.

      No hay una manera confiable de resincronizar entre la línea de tiempo virtual ideal y la línea de tiempo de reproducción real. El seguimiento del progreso de la reproducción del flujo para la administración de publicidad y Video Analytics debe utilizar el tiempo de reproducción real, por lo que el comportamiento de la interfaz de usuario y los informes puede no rastrear con precisión el contenido de los anuncios y los medios.

   * El agente de usuario entrante para todas las solicitudes HTTP de TVSDK en esta plataforma está determinado por el dispositivo y la versión de iOS que se ejecuta en el dispositivo.

      El valor de la cadena del agente de usuario es el valor predeterminado que asigna el sistema operativo.

## Prácticas recomendadas {#section_tvsdk_best_practices}

Estas son las prácticas recomendadas para TVSDK:

* Utilice HLS versión 3.0 o superior para el contenido del programa.

* Utilice la herramienta mediastreamvalidator de Apple para validar flujos VOD.

* La clase PTSDKConfig proporciona métodos para aplicar SSL en las solicitudes realizadas a servidores Primetime y DRM y Video Analytics.

Para obtener más información, consulte los métodos forceHTTPS e isForcingHTTPS de esta clase.

[!IMPORTANT]

Las solicitudes a dominios de terceros, como píxeles de seguimiento de publicidad, URL de publicidad y contenido, y solicitudes similares, no se modifican. Los proveedores de contenido y los servidores de publicidad tienen la responsabilidad de proporcionar direcciones URL compatibles con HTTPS.