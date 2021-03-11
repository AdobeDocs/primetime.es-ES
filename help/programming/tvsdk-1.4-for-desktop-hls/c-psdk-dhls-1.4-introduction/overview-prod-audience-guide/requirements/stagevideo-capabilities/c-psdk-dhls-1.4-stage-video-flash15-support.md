---
description: A partir del Flash 15 y posteriores, cuando el procesamiento de hardware con StageVideo no está disponible, StageVideo vuelve a un objeto StageVideo de software sin problemas.
title: Compatibilidad de Flash 15 con StageVideo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---


# Compatibilidad con Flash 15 para StageVideo{#flash-support-for-stagevideo}

A partir del Flash 15 y posteriores, cuando el procesamiento de hardware con StageVideo no está disponible, StageVideo vuelve a un objeto StageVideo de software sin problemas.

Tenga en cuenta la siguiente información sobre la alternativa de Flash 15 StageVideo al software:

* No es necesario realizar ningún cambio en el código en la aplicación.
* No es necesario cambiar TVSDK.

   No necesita una actualización de TVSDK para utilizar StageVideo como alternativa al software.
* Es necesario volver a compilar las aplicaciones para el Flash 15.
* Las aplicaciones que recompile para el Flash 15 seguirán funcionando con el Flash 14 y versiones anteriores, siempre que estas aplicaciones no utilicen ninguna API nueva que se haya introducido en el Flash Player 15.

   Si la aplicación Flash 14 necesita utilizar una nueva API de Flash 15, debe llamar dinámicamente a la API con una conversión al tipo de objeto, de modo que la aplicación no falle en el Flash Player 14 durante la ejecución.

## Superposiciones HTML {#html-overlays}

En el Flash 15 y posteriores, puede mantener una visualización perfecta de las superposiciones HTML cuando StageVideo de hardware deja de estar disponible y vuelve al software StageVideo. Para habilitar esta función, establezca `wmode=opaque`.

Algunos exploradores más antiguos no admiten la aceleración de hardware. Para obtener más información sobre estos requisitos, consulte [Requisitos mínimos de StageVideo](../../../../../tvsdk-1.4-for-desktop-hls/c-psdk-dhls-1.4-introduction/overview-prod-audience-guide/requirements/stagevideo-capabilities/r-psdk-dhls-1.4-requirements-stage-video.md). Cuando establece `wmode=opaque`, el vídeo se procesa con el software StageVideo, que puede afectar al rendimiento. Normalmente, si se configura `wmode=direct` directamente, el vídeo se procesa en la GPU, lo que mejora el rendimiento. Sin embargo, esta opción también anula las superposiciones HTML.
