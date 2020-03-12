---
description: Para utilizar TVSDK de forma más eficaz, debe tener en cuenta determinados detalles de su funcionamiento y seguir determinadas prácticas recomendadas.
seo-description: Para utilizar TVSDK de forma más eficaz, debe tener en cuenta determinados detalles de su funcionamiento y seguir determinadas prácticas recomendadas.
seo-title: Consideraciones y prácticas recomendadas
title: Consideraciones y prácticas recomendadas
uuid: 62a5d641-6f37-4e4d-bbc2-414bf3681d9c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Consideraciones y prácticas recomendadas{#considerations-and-best-practices}

Para utilizar TVSDK de forma más eficaz, debe tener en cuenta determinados detalles de su funcionamiento y seguir determinadas prácticas recomendadas.

## Consideraciones {#section_tvsdk_considerations}

Recuerde la siguiente información al utilizar TVSDK:

* Adobe Primetime no funciona con emuladores o simuladores.

   Debe utilizar dispositivos reales para realizar pruebas.
* La reproducción solo es compatible con el contenido de HTTP Live Streaming (HLS).
* El contenido de vídeo principal se puede multiplexar, donde los flujos de vídeo y audio están en la misma representación, o no son multiplexados, donde los flujos de audio y vídeo están en representaciones independientes.
* La API de TVSDK se implementa en ActionScript.
* La reproducción de vídeo requiere el motor de vídeo de Adobe (AVE). Esto afecta a cómo y cuándo se puede acceder a los recursos de medios:

   * Los subtítulos opcionales son compatibles en la medida en que lo proporcione el AVE.
   * Según la precisión del codificador, la duración real del medio codificado puede diferir de las duraciones registradas en el manifiesto del recurso de flujo.

      No hay una manera confiable de resincronizar entre la línea de tiempo virtual ideal y la línea de tiempo de reproducción real. El seguimiento del progreso de la reproducción del flujo para la administración de publicidad y Video Analytics debe utilizar el tiempo de reproducción real, por lo que el comportamiento de la interfaz de usuario y los informes puede no rastrear con precisión el contenido de los anuncios y los medios.
   * El nombre del agente de usuario entrante para todas las solicitudes HTTP de TVSDK en esta plataforma se asigna al siguiente patrón de cadena:

      ```
      "Adobe Flash Player"
      ```

## Prácticas recomendadas {#section_tvsdk_best_practices}

Estas son las prácticas recomendadas para TVSDK:

* Utilice HLS versión 3.0 o superior para el contenido del programa.
* Para TVSDK 1.4 para DHLS, la carga de anuncios diferida está activada de forma predeterminada.

   Para el contenido sin previo lanzamiento o con mitad de rollo, puede usar `AdvertisingMetadata.delayAdLoading` para acelerar aún más la carga de contenido.

