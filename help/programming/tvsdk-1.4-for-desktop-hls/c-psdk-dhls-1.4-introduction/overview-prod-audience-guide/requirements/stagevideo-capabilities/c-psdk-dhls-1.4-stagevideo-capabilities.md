---
description: En dispositivos que admiten la aceleración de GPU (hardware), puede utilizar un objeto flash.media.StageVideo para procesar vídeo en el hardware del dispositivo. La disponibilidad de StageVideo depende de las versiones y capacidades de diferentes partes del sistema, incluyendo Flash Player, hardware de vídeo, sistema operativo, controladores, navegador, conexión de red y contexto de visualización.
title: Funciones y restricciones de StageVideo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# Información general {#stagevideo-capabilities-and-restrictions-overview}

En dispositivos que admiten la aceleración de GPU (hardware), puede utilizar un objeto flash.media.StageVideo para procesar vídeo en el hardware del dispositivo. La disponibilidad de StageVideo depende de las versiones y capacidades de diferentes partes del sistema, incluyendo Flash Player, hardware de vídeo, sistema operativo, controladores, navegador, conexión de red y contexto de visualización.

El `StageVideo` permite aprovechar la aceleración de hardware para presentar vídeo en el nivel de rendimiento más alto posible para un dispositivo. Disponibilidad y rendimiento de `StageVideo` se ve afectado por los siguientes factores:

* **Aceleración de hardware** - Cuando la aceleración de hardware está disponible, `StageVideo` procesa el vídeo en el hardware del dispositivo. Cuando la aceleración de hardware no está disponible, la variable `StageVideo` responde depende de la versión del Flash que esté ejecutando:

   * *Flash 15 y posterior* - Cuando la aceleración por hardware no está disponible, `StageVideo` vuelve al software y no tiene que hacer nada.

     >[!TIP]
     >
     >Cuando la aceleración de hardware no está disponible, el rendimiento puede degradarse significativamente.

   * *Flash 14 y anteriores* - Cuando la aceleración por hardware no está disponible, `StageVideo` deja de estar disponible. En un pequeño conjunto de configuraciones en las que la aceleración de hardware no es compatible con el explorador o la GPU, o está desactivada en el Flash Player, la visualización de vídeo con la pila HLS de TVSDK fallará. En el *HDS* canalización, puede cambiar de `StageVideo` a una alternativa, como el objeto Video, que procesa vídeo en la CPU.

* **Contexto de presentación** - Durante la visualización de pantalla completa, `StageVideo` siempre está disponible y el rendimiento estará en el nivel máximo disponible en el dispositivo. Cuando no se ve a pantalla completa, el vídeo de presentación se encuentra en el contexto del explorador, donde se utilizan la configuración y las funciones de este.

* **wmode** : En el contexto del explorador, la variable `wmode` la configuración es crítica para el rendimiento. El Adobe recomienda que mantenga `wmode` establezca en `direct` para garantizar el mejor rendimiento posible en el contexto del explorador.

  >[!NOTE]
  >
  >La combinación de factores que incluyen `wmode`, `StageVideo`, y el Flash generan diferentes capacidades y restricciones, en función de la velocidad con la que se ejecute el hardware y de la versión del Flash que utilice.

   * *Flash 15 y posterior* - `StageVideo` está disponible con todos los disponibles `wmode` configuración. Sin embargo, si establece `wmode` a una configuración distinta de `direct`, el rendimiento será menor.

   * *Flash 14 y anteriores* - Si establece `wmode` a una configuración distinta de `direct`, `StageVideo` no está disponible en todos los navegadores.
