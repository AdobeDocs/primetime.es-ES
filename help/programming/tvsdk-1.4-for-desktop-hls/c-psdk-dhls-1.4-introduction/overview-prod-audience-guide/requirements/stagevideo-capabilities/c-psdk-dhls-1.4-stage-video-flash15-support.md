---
description: A partir del Flash 15 y versiones posteriores, cuando el procesamiento de hardware con StageVideo no está disponible, StageVideo vuelve sin problemas a un objeto StageVideo de software.
title: Compatibilidad con Flash 15 para StageVideo
exl-id: 23ef0806-3aa5-4c48-a4f7-4ad9b72bdcc9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---

# Compatibilidad con Flash 15 para StageVideo{#flash-support-for-stagevideo}

A partir del Flash 15 y versiones posteriores, cuando el procesamiento de hardware con StageVideo no está disponible, StageVideo vuelve sin problemas a un objeto StageVideo de software.

Tenga en cuenta la siguiente información sobre la alternativa de Flash 15 StageVideo al software:

* No es necesario realizar cambios en el código de su aplicación.
* No se requiere ningún cambio en TVSDK.

   No es necesario actualizar el SDK de TVSDK para utilizar StageVideo como alternativa al software.
* Sus aplicaciones necesitan ser recompiladas para el Flash 15.
* Las aplicaciones que recompile para el Flash 15 seguirán funcionando con el Flash 14 y versiones anteriores, siempre que estas aplicaciones no utilicen ninguna API nueva incluida en el Flash Player 15.

   Si la aplicación de Flash 14 necesita utilizar una nueva API de Flash 15, debe llamar dinámicamente a la API con una conversión al tipo de objeto, de modo que la aplicación no falle en el Flash Player 14 durante la ejecución.

## Superposiciones de HTML {#html-overlays}

En Flash 15 y versiones posteriores, puede mantener una visualización perfecta de las superposiciones del HTML cuando el hardware StageVideo deja de estar disponible y vuelve al software StageVideo. Para habilitar esta función, establezca `wmode=opaque`.

Algunos exploradores más antiguos no admiten la aceleración de hardware. Para obtener más información sobre estos requisitos, consulte [Requisitos mínimos de StageVideo](../../../../../tvsdk-1.4-for-desktop-hls/c-psdk-dhls-1.4-introduction/overview-prod-audience-guide/requirements/stagevideo-capabilities/r-psdk-dhls-1.4-requirements-stage-video.md). Cuando se establece `wmode=opaque`Además, el vídeo se procesa con el software StageVideo, que puede afectar al rendimiento. Normalmente, configurar `wmode=direct` procesa vídeo directamente en la GPU, lo que mejora considerablemente el rendimiento. Sin embargo, esta opción también anula las superposiciones del HTML.
