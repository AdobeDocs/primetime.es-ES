---
description: Una vez que se ha utilizado una vista de MediaPlayer para reproducir vídeo, puede ocultarlo y mostrarlo de nuevo mediante un método TVSDK o manualmente.
title: Ocultar una vista de vídeo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 1%

---


# Ocultar una vista de vídeo{#hide-a-video-view}

Una vez que se ha utilizado una vista de MediaPlayer para reproducir vídeo, puede ocultarlo y mostrarlo de nuevo mediante un método TVSDK o manualmente.

Debe pausar un vídeo antes de borrarlo o moverlo desde la pantalla.
* Opción 1: Borre el marco de vídeo con `MediaPlayer.clearVideo` &#x200B; y sustituya el marco más adelante.
   * Pause el vídeo que desee ocultar.
   * Elimine el fotograma de vídeo mostrado llamando a `MediaPlayer.clearVideo`.
   * Para restablecer el `MediaPlayer` para que se pueda reproducir de nuevo, llame a `replaceCurrentResource` o `replaceCurrentItem`.
* Opción 2: Desplace la vista `MediaPlayer` de la pantalla y muévala más tarde sin tener que reemplazarla.
   * Pause el vídeo que desee ocultar.
   * Saque la vista del escenario. Por ejemplo:

      ```
      view.x = -300; 
      view.y = -300;
      ```

   * Para volver a mostrar el vídeo, mueva la vista de nuevo al escenario.
