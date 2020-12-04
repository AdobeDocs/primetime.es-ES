---
description: Para utilizar TVSDK de forma más eficaz, debe tener en cuenta determinados detalles de su funcionamiento y seguir determinadas prácticas recomendadas.
seo-description: Para utilizar TVSDK de forma más eficaz, debe tener en cuenta determinados detalles de su funcionamiento y seguir determinadas prácticas recomendadas.
seo-title: Consideraciones y prácticas recomendadas
title: Consideraciones y prácticas recomendadas
uuid: 049da1f4-028b-49d2-9ebd-e5d9edcbaf8a
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# Consideraciones y prácticas recomendadas{#considerations-and-best-practices}

Para utilizar TVSDK de forma más eficaz, debe tener en cuenta determinados detalles de su funcionamiento y seguir determinadas prácticas recomendadas.

## Consideraciones {#section_tvsdk_considerations}

Recuerde la siguiente información al utilizar TVSDK:

* La API de TVSDK se implementa en Java.
* Adobe Primetime no funciona actualmente en emuladores de Android.

   Debe utilizar dispositivos reales para realizar pruebas.
* La reproducción solo se admite para el contenido de HTTP Live Streaming (HLS).
* El contenido principal de vídeo se puede multiplexar (flujos de audio y vídeo en la misma representación) o no multiplexar (flujos de audio y vídeo en representaciones independientes).
* Actualmente, es necesario ejecutar la mayoría de las operaciones de API de TVSDK en el subproceso de interfaz de usuario, que es el subproceso principal de Android.

   Las operaciones que se ejecutan correctamente en el subproceso principal pueden generar un error y salir cuando se ejecutan en un subproceso en segundo plano.
* La reproducción de vídeo requiere el motor de vídeo Adobe (AVE). Esto afecta a cómo y cuándo se puede acceder a los recursos de medios:

   * Los subtítulos opcionales son compatibles en la medida en que lo proporcione el AVE.
   * Según la precisión del codificador, la duración real del medio codificado puede diferir de las duraciones registradas en el manifiesto del recurso de flujo.

      No hay una manera confiable de resincronizar entre la línea de tiempo virtual ideal y la línea de tiempo de reproducción real. El seguimiento del progreso de la reproducción del flujo para la administración de anuncios y Video Analytics debe utilizar el tiempo de reproducción real, por lo que el comportamiento de la interfaz de usuario y el sistema de informes puede no rastrear con precisión el contenido de los medios y los anuncios.
   * El nombre del agente de usuario entrante para todas las solicitudes de medios de TVSDK en esta plataforma se asigna al siguiente patrón de cadena:

   ```
   "Adobe Primetime/" + 
   <varname>
   originalUserAgent
   </varname> 
   ```

   Todas las llamadas relacionadas con la publicidad utilizan el agente de usuario predeterminado de Android o el agente de usuario personalizado si lo establece al configurar los metadatos de inserción de publicidad.

## Prácticas recomendadas {#section_tvsdk_best_practices}

Estas son las prácticas recomendadas para TVSDK:

* Utilice HLS versión 3.0 o superior para el contenido de programa.
* Ejecute la mayoría de las operaciones de TVSDK en el subproceso principal (UI), no en los subprocesos en segundo plano.
* Para TVSDK 2.5 para Android, la resolución de publicidad diferida está activada de forma predeterminada.

   Para el contenido que no tiene preversión ni mitad de lista, puede utilizar `AdvertisingMetadata.setPreroll(false)` para acelerar la carga de contenido.
