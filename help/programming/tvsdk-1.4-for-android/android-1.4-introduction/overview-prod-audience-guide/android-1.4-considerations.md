---
description: Para utilizar TVSDK de forma más eficaz, debe tener en cuenta determinados detalles de su funcionamiento y seguir determinadas prácticas recomendadas.
seo-description: Para utilizar TVSDK de forma más eficaz, debe tener en cuenta determinados detalles de su funcionamiento y seguir determinadas prácticas recomendadas.
seo-title: Consideraciones y prácticas recomendadas
title: Consideraciones y prácticas recomendadas
uuid: e698ae09-280b-4406-a9b8-4f468b7a6b9c
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Consideraciones y prácticas recomendadas{#considerations-and-best-practices}

Para utilizar TVSDK de forma más eficaz, debe tener en cuenta determinados detalles de su funcionamiento y seguir determinadas prácticas recomendadas.

## Consideraciones {#section_tvsdk_considerations}

Recuerde la siguiente información al utilizar TVSDK:

* Adobe Primetime no funciona actualmente en emuladores de Android.

   Debe utilizar dispositivos reales para realizar pruebas.
* La reproducción solo es compatible con el contenido de HTTP Live Streaming (HLS).
* El contenido de vídeo principal se puede multiplexar, donde los flujos de vídeo y audio están en la misma representación, o no son multiplexados, donde los flujos de audio y vídeo están en representaciones independientes.
* La API de TVSDK se implementa en Java.
* Actualmente, es necesario ejecutar la mayoría de las operaciones de API de TVSDK en el subproceso de interfaz de usuario, que es el subproceso principal de Android.

   Las operaciones que se ejecutan correctamente en el subproceso principal pueden generar un error y salir cuando se ejecutan en un subproceso en segundo plano.
* La reproducción de vídeo requiere el motor de vídeo de Adobe (AVE). Esto afecta a cómo y cuándo se puede acceder a los recursos de medios:

   * Los subtítulos opcionales son compatibles en la medida en que lo proporcione el AVE.
   * Según la precisión del codificador, la duración real del medio codificado puede diferir de las duraciones registradas en el manifiesto del recurso de flujo.

      No hay una manera confiable de volver a sincronizar entre la línea de tiempo virtual ideal y la línea de tiempo de reproducción real. El seguimiento del progreso de la reproducción del flujo para la administración de publicidad y Video Analytics debe utilizar el tiempo de reproducción real, por lo que el comportamiento de la interfaz de usuario y los informes puede no rastrear con precisión el contenido de los anuncios y los medios.
   * El nombre del agente de usuario entrante para todas las solicitudes de medios de TVSDK en esta plataforma se asigna al siguiente patrón de cadena:

      ```
      "Adobe Primetime/ + 
      <varname>
      originalUserAgent
      </varname>" 
      ```

      Todas las llamadas relacionadas con la publicidad utilizan el agente de usuario predeterminado de Android o el agente de usuario personalizado si lo establece al configurar los metadatos de inserción de publicidad.

## Prácticas recomendadas {#section_tvsdk_best_practices}

Estas son las prácticas recomendadas para TVSDK:

* Utilice HLS versión 3.0 o superior para el contenido del programa.
* Ejecute la mayoría de las operaciones de TVSDK en el subproceso principal (UI), no en los subprocesos en segundo plano.
