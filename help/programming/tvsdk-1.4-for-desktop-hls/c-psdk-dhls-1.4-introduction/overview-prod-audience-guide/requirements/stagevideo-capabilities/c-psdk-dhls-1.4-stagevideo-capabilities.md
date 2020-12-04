---
description: En dispositivos que admiten aceleración de GPU (hardware), puede utilizar un objeto flash.media.StageVideo para procesar vídeo en el hardware del dispositivo. La disponibilidad de StageVideo depende de las versiones y capacidades de diferentes partes del sistema, incluyendo Flash Player, hardware de vídeo, SO, controladores, navegador, conexión de red y contexto de visualización.
seo-description: En dispositivos que admiten aceleración de GPU (hardware), puede utilizar un objeto flash.media.StageVideo para procesar vídeo en el hardware del dispositivo. La disponibilidad de StageVideo depende de las versiones y capacidades de diferentes partes del sistema, incluyendo Flash Player, hardware de vídeo, SO, controladores, navegador, conexión de red y contexto de visualización.
seo-title: Funciones y restricciones de StageVideo
title: Funciones y restricciones de StageVideo
uuid: 7556f30b-4b9f-4258-beb6-2a4ce8f05d1a
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# Información general {#stagevideo-capabilities-and-restrictions-overview}

En dispositivos que admiten aceleración de GPU (hardware), puede utilizar un objeto flash.media.StageVideo para procesar vídeo en el hardware del dispositivo. La disponibilidad de StageVideo depende de las versiones y capacidades de diferentes partes del sistema, incluyendo Flash Player, hardware de vídeo, SO, controladores, navegador, conexión de red y contexto de visualización.

La clase `StageVideo` le permite aprovechar la aceleración de hardware para presentar vídeo con el nivel de rendimiento más alto posible para un dispositivo. La disponibilidad y el rendimiento de `StageVideo` se ven afectados por los siguientes factores:

* **Aceleración**  de hardware: cuando la aceleración de hardware está disponible,  `StageVideo` procesa el vídeo en el hardware del dispositivo. Cuando la aceleración de hardware no está disponible, la respuesta `StageVideo` depende de la versión de Flash que se esté ejecutando:

   * *Flash 15 y posterior* : cuando la aceleración de hardware no está disponible,  `StageVideo` regresa al software y no tiene que hacer nada.

      >[!TIP]
      >
      >Cuando la aceleración de hardware no está disponible, el rendimiento puede degradarse considerablemente.

   * *Flash 14 y versiones anteriores* : cuando la aceleración de hardware no está disponible,  `StageVideo` deja de estar disponible. En un pequeño conjunto de configuraciones en las que la aceleración de hardware no es compatible con el navegador o la GPU, o está desactivada en el Flash Player, la visualización de vídeo con la pila TVSDK HLS fallará. En la canalización *HDS*, puede cambiar de `StageVideo` a una alternativa, como el objeto Video, que procesa el video en la CPU.

* **Contexto**  de la presentación: durante la visualización a pantalla completa,  `StageVideo` siempre está disponible y el rendimiento estará al nivel máximo disponible en el dispositivo. Cuando no se visualiza la pantalla completa, la presentación del vídeo se incluye en el contexto del navegador, donde se utilizan la configuración y las funciones del navegador.

* **wmode** : en el contexto del navegador, la  `wmode` configuración es crítica para el rendimiento. Adobe recomienda mantener `wmode` configurado en `direct` para garantizar el mejor rendimiento posible en el contexto del explorador.

   >[!NOTE]
   >
   >La combinación de factores que incluyen `wmode`, `StageVideo` y Flash resulta en diferentes capacidades y restricciones, según la velocidad con la que se ejecute el hardware y la versión de Flash que utilice.

   * *Flash 15 y posterior* :  `StageVideo` está disponible con todos los  `wmode` ajustes disponibles. Sin embargo, si establece `wmode` en una configuración que no sea `direct`, el rendimiento será menor.

   * *Flash 14 y versiones anteriores* : si se establece  `wmode` en una configuración distinta de  `direct`, no  `StageVideo` está disponible en todos los exploradores.

