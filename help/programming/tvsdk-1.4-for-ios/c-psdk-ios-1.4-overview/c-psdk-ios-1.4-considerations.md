---
description: Para utilizar TVSDK de forma más eficaz, debe tener en cuenta ciertos detalles de su funcionamiento y seguir determinadas prácticas recomendadas.
title: Consideraciones y prácticas recomendadas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---


# Consideraciones y prácticas recomendadas{#considerations-and-best-practices}

Para utilizar TVSDK de forma más eficaz, debe tener en cuenta ciertos detalles de su funcionamiento y seguir determinadas prácticas recomendadas.

## Consideraciones {#section_tvsdk_considerations}

Recuerde la siguiente información cuando utilice TVSDK:

* Adobe Primetime no funciona en los simuladores de iOS.

   Debe utilizar dispositivos reales para realizar pruebas.
* La reproducción solo es compatible con el contenido de HTTP Live Streaming (HLS).
* El contenido de vídeo principal se puede multiplexar, ya que las emisiones de vídeo y audio se encuentran en la misma representación o no son multiplexadas, donde las emisiones de vídeo y audio se encuentran en representaciones independientes.
* La API de TVSDK se implementa en Objective-C.
* La reproducción de vídeo requiere el marco nativo de Apple AV Foundation. Esto afecta a cómo y cuándo se puede acceder a los recursos multimedia, incluidos los subtítulos cerrados y las líneas de tiempo:

   * Los ajustes de línea de tiempo no se pueden revisar después de la configuración inicial.

      Por ejemplo, un anuncio no se puede eliminar de la cronología después de reproducirse. Si el usuario vuelve a buscar en la presentación, se vuelve a reproducir el mismo anuncio aunque la política hubiera sido eliminar el anuncio.
   * En función de la precisión del codificador, la duración real del contenido codificado puede diferir de las duraciones registradas en el manifiesto del recurso de flujo.

      No hay una manera fiable de resincronizar entre la cronología virtual ideal y la cronología de reproducción real. El seguimiento del progreso de la reproducción de la emisión para la administración de anuncios y Video Analytics debe utilizar el tiempo de reproducción real, por lo que el comportamiento de la interfaz de usuario y los informes puede no rastrear con precisión el contenido de los medios y los anuncios.
   * El agente de usuario entrante para todas las solicitudes HTTP de TVSDK en esta plataforma lo determinan el dispositivo y la versión de iOS que se ejecuta en el dispositivo.

      El valor de la cadena del agente de usuario es el valor predeterminado que asigna el sistema operativo.

## Prácticas recomendadas {#section_tvsdk_best_practices}

Estas son las prácticas recomendadas para TVSDK:

* Utilice HLS versión 3.0 o superior para el contenido del programa.
* Utilice la herramienta mediastreamvalidator de Apple para validar los flujos de VOD.
* La clase `PTSDKConfig` proporciona métodos para aplicar SSL en las solicitudes realizadas a los servidores de Primetime ad decisioning, DRM y Video Analytics.

   Para obtener más información, consulte los métodos `forceHTTPS` y `isForcingHTTPS` en esta clase.

   >[!IMPORTANT]
   >
   >Las solicitudes para dominios de terceros, como píxeles de seguimiento de anuncios, URL de contenido y anuncios y solicitudes similares, no se modifican. Los proveedores de contenido y los servidores de publicidad tienen la responsabilidad de proporcionar direcciones URL compatibles con HTTPS.

