---
description: Una vez que se ha utilizado una vista de MediaPlayer para reproducir vídeo, puede ocultarla y mostrarla de nuevo mediante un método TVSDK o manualmente.
title: Ocultar una vista de vídeo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# Ocultar una vista de vídeo{#hide-a-video-view}

Una vez que se ha utilizado una vista de MediaPlayer para reproducir vídeo, puede ocultarla y mostrarla de nuevo mediante un método TVSDK o manualmente.

Debe pausar un vídeo antes de borrarlo o moverlo de la pantalla.
* Opción 1: borrar el fotograma de vídeo con `MediaPlayer.clearVideo`y reemplace el cuadro más tarde.
   * Ponga en pausa el vídeo que desee ocultar.
   * Elimine el fotograma de vídeo mostrado llamando a `MediaPlayer.clearVideo`.
   * Para restablecer el `MediaPlayer` para que se pueda reproducir de nuevo, llame a `replaceCurrentResource` o `replaceCurrentItem`.
* Opción 2: Mover el `MediaPlayer` vea la pantalla y vuelva a moverla más tarde sin tener que reemplazarla.
   * Ponga en pausa el vídeo que desee ocultar.
   * Mueva la vista fuera del escenario. Por ejemplo:

     ```
     view.x = -300; 
     view.y = -300;
     ```

   * Para volver a mostrar el vídeo, mueva la vista de nuevo al escenario.
