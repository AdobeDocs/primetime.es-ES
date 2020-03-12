---
description: A partir de Flash 15 y versiones posteriores, cuando el procesamiento por hardware con StageVideo no está disponible, StageVideo regresa sin problemas a un objeto StageVideo de software.
seo-description: A partir de Flash 15 y versiones posteriores, cuando el procesamiento por hardware con StageVideo no está disponible, StageVideo regresa sin problemas a un objeto StageVideo de software.
seo-title: Compatibilidad de Flash 15 con StageVideo
title: Compatibilidad de Flash 15 con StageVideo
uuid: 49bd8703-016e-4fda-8773-5254d4774ec6
translation-type: tm+mt
source-git-commit: fd686391df0fa711bba99bc1bc312c9ef619f184

---


# Compatibilidad de Flash 15 con StageVideo{#flash-support-for-stagevideo}

A partir de Flash 15 y versiones posteriores, cuando el procesamiento por hardware con StageVideo no está disponible, StageVideo regresa sin problemas a un objeto StageVideo de software.

Considere la siguiente información sobre el respaldo de Flash 15 StageVideo al software:

* No se requieren cambios en el código en la aplicación.
* No se requiere ningún cambio en TVSDK.

   No necesita una actualización de TVSDK para utilizar el complemento StageVideo en software.
* Es necesario volver a compilar las aplicaciones para Flash 15.
* Las aplicaciones que recompila para Flash 15 seguirán funcionando con Flash 14 y versiones anteriores, siempre que estas aplicaciones no utilicen ninguna API nueva que se introdujera en Flash Player 15.

   Si la aplicación Flash 14 necesita utilizar una nueva API de Flash 15, debe llamar dinámicamente a la API con una conversión al tipo de objeto para que la aplicación no falle en Flash Player 14 durante la ejecución.

## Superposiciones HTML {#html-overlays}

En Flash 15 y versiones posteriores, se puede mantener una visualización transparente de las superposiciones HTML cuando el hardware StageVideo deja de estar disponible y regresa al software StageVideo. Para activar esta función, establezca `wmode=opaque`.

Algunos exploradores antiguos no admiten la aceleración de hardware. Para obtener más información sobre estos requisitos, consulte Requisitos [mínimos de](../../../../../tvsdk-1.4-for-desktop-hls/c-psdk-dhls-1.4-introduction/overview-prod-audience-guide/requirements/stagevideo-capabilities/r-psdk-dhls-1.4-requirements-stage-video.md)StageVideo. Cuando se configura `wmode=opaque`, el vídeo se procesa con el software StageVideo, que puede afectar al rendimiento. Normalmente, la configuración `wmode=direct` directa procesa el vídeo en una GPU, lo que mejora el rendimiento. Sin embargo, esta opción también anula las superposiciones HTML.
