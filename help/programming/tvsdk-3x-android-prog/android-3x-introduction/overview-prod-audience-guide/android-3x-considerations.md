---
description: Para utilizar TVSDK de forma más eficaz, debe tener en cuenta determinados detalles de su funcionamiento y seguir determinadas prácticas recomendadas.
title: Consideraciones y prácticas recomendadas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# Consideraciones y prácticas recomendadas {#considerations-and-best-practices}

Para utilizar TVSDK de forma más eficaz, debe tener en cuenta determinados detalles de su funcionamiento y seguir determinadas prácticas recomendadas.

## Consideraciones {#section_tvsdk_considerations}

Recuerde la siguiente información al utilizar TVSDK:

* La API de TVSDK se implementa en Java.
* Adobe Primetime no funciona actualmente en emuladores de Android.

  Debe utilizar dispositivos reales para realizar pruebas.
* La reproducción solo es compatible con contenido de flujo en directo HTTP (HLS).
* El contenido del vídeo principal puede ser multiplexado (flujos de vídeo y audio en la misma representación) o no multiplexado (flujos de vídeo y audio en representaciones independientes).
* Actualmente, debe ejecutar la mayoría de las operaciones de API de TVSDK en el subproceso de la interfaz de usuario, que es el principal subproceso de Android.

  Las operaciones que se ejecutan correctamente en el subproceso principal pueden generar un error y salir cuando se ejecutan en un subproceso en segundo plano.
* La reproducción de vídeo requiere Adobe Video Engine (AVE). Esto afecta a cómo y cuándo se puede acceder a los recursos de medios:

   * Los subtítulos opcionales son compatibles en la medida en que los proporciona el AVE.
   * En función de la precisión del codificador, la duración real de los medios codificados puede diferir de las duraciones registradas en el manifiesto de recursos de flujo.

     No existe una forma fiable de volver a sincronizar la escala de tiempo virtual ideal con la de reproducción real. El seguimiento del progreso de la reproducción del flujo para la gestión de anuncios y Video Analytics debe utilizar el tiempo de reproducción real, por lo que es posible que los informes y el comportamiento de la interfaz de usuario no rastreen con precisión el contenido de los medios y los anuncios.
   * El nombre del agente de usuario entrante para todas las solicitudes de medios del TVSDK en esta plataforma se asigna al siguiente patrón de cadena:

     ```
     "Adobe Primetime/" + originalUserAgent
     ```

     Todas las llamadas relacionadas con anuncios utilizan el agente de usuario predeterminado de Android o el agente de usuario personalizado si lo establece al configurar los metadatos de inserción de anuncios.

## Prácticas recomendadas {#section_tvsdk_best_practices}

Estas son las prácticas recomendadas para TVSDK:

* Utilice la versión 3.0 o superior de HLS para el contenido del programa.
* Ejecute la mayoría de las operaciones de TVSDK en el subproceso principal (IU), no en los subprocesos en segundo plano.
* Para TVSDK 3.0 para Android, la resolución de anuncios diferidos está activada de forma predeterminada.

Para contenido sin anuncio previo o anuncio durante la emisión, puede utilizar `AdvertisingMetadata.setPreroll(false)` para acelerar la carga de contenido.
