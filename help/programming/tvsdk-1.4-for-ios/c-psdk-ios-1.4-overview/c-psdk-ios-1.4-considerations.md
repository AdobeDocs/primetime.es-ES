---
description: Para utilizar TVSDK de forma más eficaz, debe tener en cuenta determinados detalles de su funcionamiento y seguir determinadas prácticas recomendadas.
title: Consideraciones y prácticas recomendadas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---

# Consideraciones y prácticas recomendadas{#considerations-and-best-practices}

Para utilizar TVSDK de forma más eficaz, debe tener en cuenta determinados detalles de su funcionamiento y seguir determinadas prácticas recomendadas.

## Consideraciones {#section_tvsdk_considerations}

Recuerde la siguiente información al utilizar TVSDK:

* Adobe Primetime no funciona en simuladores de iOS.

  Debe utilizar dispositivos reales para realizar pruebas.
* La reproducción solo es compatible con contenido de flujo en directo HTTP (HLS).
* El contenido del vídeo principal puede ser multiplexado, donde los flujos de vídeo y audio están en la misma representación, o no multiplexado, donde los flujos de vídeo y audio están en representaciones independientes.
* La API de TVSDK se implementa en Objective-C.
* La reproducción de vídeo requiere el módulo nativo de Apple AV Foundation. Esto afecta a cómo y cuándo se puede acceder a los recursos de medios, incluidos subtítulos y cronologías:

   * Los ajustes de cronología no se pueden revisar después de la configuración inicial.

     Por ejemplo, un anuncio no se puede eliminar de la cronología una vez reproducido. Si el usuario busca nuevamente en la presentación, el mismo anuncio se reproduce de nuevo aunque la política hubiera sido eliminar el anuncio.
   * En función de la precisión del codificador, la duración real de los medios codificados puede diferir de las duraciones registradas en el manifiesto de recursos de flujo.

     No existe una forma fiable de volver a sincronizar la escala de tiempo virtual ideal con la de reproducción real. El seguimiento del progreso de la reproducción del flujo para la gestión de anuncios y Video Analytics debe utilizar el tiempo de reproducción real, por lo que es posible que los informes y el comportamiento de la interfaz de usuario no rastreen con precisión el contenido de los medios y los anuncios.
   * El agente de usuario entrante para todas las solicitudes HTTP de TVSDK en esta plataforma está determinado por el dispositivo y la versión de iOS que se ejecuta en el dispositivo.

     El valor predeterminado de la cadena del agente de usuario es lo que asigna el sistema operativo.

## Prácticas recomendadas {#section_tvsdk_best_practices}

Estas son las prácticas recomendadas para TVSDK:

* Utilice la versión 3.0 o superior de HLS para el contenido del programa.
* Utilice la herramienta mediastreamvalidator de Apple para validar flujos de VOD.
* El `PTSDKConfig` proporciona métodos para aplicar SSL en solicitudes realizadas en los servidores de Primetime ad Decisioning, DRM y Video Analytics.

  Para obtener más información, consulte la `forceHTTPS` y `isForcingHTTPS` métodos de esta clase.

  >[!IMPORTANT]
  >
  >Las solicitudes a dominios de terceros, como píxeles de seguimiento de publicidad, URL de contenido y publicidad, y solicitudes similares, no se modifican. Es responsabilidad de los proveedores de contenido y de los servidores de publicidad proporcionar las direcciones URL compatibles mediante HTTPS.
