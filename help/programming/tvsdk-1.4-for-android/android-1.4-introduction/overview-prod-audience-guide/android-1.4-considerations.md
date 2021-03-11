---
description: Para utilizar TVSDK de forma más eficaz, debe tener en cuenta ciertos detalles de su funcionamiento y seguir determinadas prácticas recomendadas.
title: Consideraciones y prácticas recomendadas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---


# Consideraciones y prácticas recomendadas{#considerations-and-best-practices}

Para utilizar TVSDK de forma más eficaz, debe tener en cuenta ciertos detalles de su funcionamiento y seguir determinadas prácticas recomendadas.

## Consideraciones {#section_tvsdk_considerations}

Recuerde la siguiente información cuando utilice TVSDK:

* Adobe Primetime no funciona actualmente en emuladores de Android.

   Debe utilizar dispositivos reales para realizar pruebas.
* La reproducción solo es compatible con el contenido de HTTP Live Streaming (HLS).
* El contenido de vídeo principal se puede multiplexar, ya que las emisiones de vídeo y audio se encuentran en la misma representación, o no son multiplexadas, donde las emisiones de vídeo y audio se encuentran en representaciones independientes.
* La API de TVSDK se implementa en Java.
* Actualmente, es necesario ejecutar la mayoría de las operaciones de API de TVSDK en el subproceso de interfaz de usuario, que es el subproceso principal de Android.

   Las operaciones que se ejecutan correctamente en el subproceso principal pueden generar un error y salir cuando se ejecutan en un subproceso en segundo plano.
* La reproducción de vídeo requiere el motor de vídeo de Adobe (AVE). Esto afecta a cómo y cuándo se puede acceder a los recursos de medios:

   * Los subtítulos se admiten en la medida en que lo proporcione el AVE.
   * En función de la precisión del codificador, la duración real del contenido codificado puede diferir de las duraciones registradas en el manifiesto del recurso de flujo.

      No hay una manera fiable de volver a sincronizar entre la cronología virtual ideal y la cronología de emisión real. El seguimiento del progreso de la reproducción de la emisión para la administración de anuncios y Video Analytics debe utilizar el tiempo de reproducción real, por lo que el comportamiento de la interfaz de usuario y los informes puede no rastrear con precisión el contenido de los medios y los anuncios.
   * El nombre del agente de usuario entrante para todas las solicitudes de medios de TVSDK en esta plataforma se asigna al siguiente patrón de cadena:

      ```
      "Adobe Primetime/ + 
      <varname>
      originalUserAgent
      </varname>" 
      ```

      Todas las llamadas relacionadas con anuncios utilizan el agente de usuario predeterminado de Android o el agente de usuario personalizado si lo establece al configurar los metadatos de inserción de anuncios.

## Prácticas recomendadas {#section_tvsdk_best_practices}

Estas son las prácticas recomendadas para TVSDK:

* Utilice HLS versión 3.0 o superior para el contenido del programa.
* Ejecute la mayoría de las operaciones de TVSDK en el subproceso principal (IU), no en los subprocesos en segundo plano.
