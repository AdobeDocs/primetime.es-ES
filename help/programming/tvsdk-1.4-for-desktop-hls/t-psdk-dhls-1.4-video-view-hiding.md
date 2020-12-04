---
description: Una vez que se ha utilizado una vista de MediaPlayer para reproducir vídeo, puede ocultarlo y mostrarlo de nuevo mediante un método TVSDK o manualmente.
seo-description: Una vez que se ha utilizado una vista de MediaPlayer para reproducir vídeo, puede ocultarlo y mostrarlo de nuevo mediante un método TVSDK o manualmente.
seo-title: Ocultar una vista de vídeo
title: Ocultar una vista de vídeo
uuid: 7cc02bf4-41ee-4af0-98ba-df070b50b88d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 1%

---


# Ocultar una vista de vídeo{#hide-a-video-view}

Una vez que se ha utilizado una vista de MediaPlayer para reproducir vídeo, puede ocultarlo y mostrarlo de nuevo mediante un método TVSDK o manualmente.

Debe pausar un vídeo antes de borrarlo o moverlo desde la pantalla.
* Opción 1: Borre el fotograma de vídeo con `MediaPlayer.clearVideo` &#x200B; y reemplace el fotograma más adelante.
   * Pause el vídeo que desee ocultar.
   * Elimine el fotograma de vídeo mostrado llamando a `MediaPlayer.clearVideo`.
   * Para restablecer el `MediaPlayer` para que se pueda reproducir nuevamente, llame a `replaceCurrentResource` o `replaceCurrentItem`.
* Opción 2: Mueva la vista `MediaPlayer` de la pantalla y muévala más tarde sin tener que reemplazarla.
   * Pause el vídeo que desee ocultar.
   * Mueva la vista fuera del escenario. Por ejemplo:

      ```
      view.x = -300; 
      view.y = -300;
      ```

   * Para volver a mostrar el vídeo, mueva la vista al escenario.
