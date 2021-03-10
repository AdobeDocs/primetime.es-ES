---
description: En los dispositivos que admiten aceleración de GPU (hardware), puede utilizar un objeto flash.media.StageVideo para procesar vídeo en el hardware del dispositivo. La disponibilidad de StageVideo depende de las versiones y capacidades de diferentes partes del sistema, incluyendo Flash Player, hardware de vídeo, SO, controladores, navegador, conexión de red y contexto de visualización.
title: Capacidades y restricciones de StageVideo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# Información general {#stagevideo-capabilities-and-restrictions-overview}

En los dispositivos que admiten aceleración de GPU (hardware), puede utilizar un objeto flash.media.StageVideo para procesar vídeo en el hardware del dispositivo. La disponibilidad de StageVideo depende de las versiones y capacidades de diferentes partes del sistema, incluyendo Flash Player, hardware de vídeo, SO, controladores, navegador, conexión de red y contexto de visualización.

La clase `StageVideo` le permite aprovechar la aceleración de hardware para presentar el vídeo al nivel de rendimiento más alto posible para un dispositivo. La disponibilidad y el rendimiento de `StageVideo` se ven afectados por los siguientes factores:

* **Aceleración de hardware** : cuando la aceleración de hardware está disponible,  `StageVideo` procesa el vídeo en el hardware del dispositivo. Cuando la aceleración de hardware no está disponible, la respuesta de `StageVideo` depende de la versión de Flash que esté ejecutando:

   * *Flash 15 y posteriores* : cuando la aceleración de hardware no está disponible,  `StageVideo` vuelve al software y no tiene que hacer nada.

      >[!TIP]
      >
      >Cuando la aceleración de hardware no está disponible, el rendimiento puede degradarse significativamente.

   * *Flash 14 y anteriores* : cuando la aceleración de hardware no está disponible,  `StageVideo` deja de estar disponible. En un pequeño conjunto de configuraciones en las que la aceleración de hardware no es compatible con el navegador o la GPU, o está desactivada en el Flash Player, la visualización de vídeo con la pila HLS TVSDK fallará. En la canalización *HDS*, puede cambiar de `StageVideo` a una alternativa, como el objeto Video, que procesa el vídeo en la CPU.

* **Contexto de presentación** : durante la visualización de pantalla completa, siempre  `StageVideo` está disponible y el rendimiento estará al nivel máximo disponible en el dispositivo. Al no ver la pantalla completa, la presentación del vídeo entra dentro del contexto del explorador, donde se utilizan la configuración y las capacidades del explorador.

* **wmode** : en el contexto del explorador, la  `wmode` configuración es crítica para el rendimiento. Adobe recomienda mantener `wmode` establecido en `direct` para garantizar el mejor rendimiento posible en el contexto del explorador.

   >[!NOTE]
   >
   >La combinación de factores que incluyen `wmode`, `StageVideo` y el Flash resultan en diferentes capacidades y restricciones, dependiendo de la velocidad con la que se ejecute el hardware y de la versión de Flash que esté utilizando.

   * *Flash 15 y posteriores* :  `StageVideo` está disponible con todos los  `wmode` ajustes disponibles. Sin embargo, si establece `wmode` en un valor distinto de `direct`, el rendimiento será menor.

   * *Flash 14 y versiones anteriores* : Si se establece  `wmode` en una configuración distinta de  `direct`, no  `StageVideo` está disponible en todos los exploradores.

