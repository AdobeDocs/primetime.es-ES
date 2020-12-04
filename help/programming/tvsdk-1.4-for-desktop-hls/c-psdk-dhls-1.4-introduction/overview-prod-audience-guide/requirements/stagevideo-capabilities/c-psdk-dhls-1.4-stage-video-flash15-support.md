---
description: A partir del Flash 15 y versiones posteriores, cuando el procesamiento por hardware con StageVideo no está disponible, StageVideo regresa sin problemas a un objeto StageVideo de software.
seo-description: A partir del Flash 15 y versiones posteriores, cuando el procesamiento por hardware con StageVideo no está disponible, StageVideo regresa sin problemas a un objeto StageVideo de software.
seo-title: Compatibilidad de Flash 15 con StageVideo
title: Compatibilidad de Flash 15 con StageVideo
uuid: 49bd8703-016e-4fda-8773-5254d4774ec6
translation-type: tm+mt
source-git-commit: fd686391df0fa711bba99bc1bc312c9ef619f184
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---


# Compatibilidad de Flash 15 para StageVideo{#flash-support-for-stagevideo}

A partir del Flash 15 y versiones posteriores, cuando el procesamiento por hardware con StageVideo no está disponible, StageVideo regresa sin problemas a un objeto StageVideo de software.

Tenga en cuenta la siguiente información sobre el Flash 15 StageVideo de reserva en software:

* No se requieren cambios en el código en la aplicación.
* No se requiere ningún cambio en TVSDK.

   No necesita una actualización de TVSDK para utilizar el complemento StageVideo en software.
* Es necesario volver a compilar las aplicaciones para Flash 15.
* Las aplicaciones que recompila para Flash 15 seguirán funcionando con Flash 14 y versiones anteriores, siempre que estas aplicaciones no utilicen ninguna API nueva que se introdujera en Flash Player 15.

   Si la aplicación Flash 14 necesita utilizar una nueva API de Flash 15, debe llamar dinámicamente a la API con una conversión al tipo de objeto, de modo que la aplicación no falle en Flash Player 14 en tiempo de ejecución.

## Superposiciones HTML {#html-overlays}

En Flash 15 y versiones posteriores, puede mantener una visualización transparente de las superposiciones HTML cuando StageVideo de hardware deja de estar disponible y vuelve a estar en el software StageVideo. Para habilitar esta función, configure `wmode=opaque`.

Algunos exploradores antiguos no admiten la aceleración de hardware. Para obtener más información sobre estos requisitos, consulte [Requisitos mínimos de StageVideo](../../../../../tvsdk-1.4-for-desktop-hls/c-psdk-dhls-1.4-introduction/overview-prod-audience-guide/requirements/stagevideo-capabilities/r-psdk-dhls-1.4-requirements-stage-video.md). Cuando establece `wmode=opaque`, el vídeo se procesa con el software StageVideo, que puede afectar al rendimiento. Normalmente, al configurar `wmode=direct` directamente se procesa el vídeo en la GPU, lo que resulta en un rendimiento mucho mejor. Sin embargo, esta opción también anula las superposiciones HTML.
