---
description: Puede utilizar las superposiciones de HTML con StageVideo para mostrar los elementos de la interfaz de usuario en el plano de vídeo de la lista de visualización de Flash. Este plano está por encima del plano de StageVideo, por lo que StageVideo siempre se muestra detrás de los elementos de la lista de visualización de Flash.
title: Superposiciones de vídeo y HTML de fase
exl-id: 6beda4c8-0981-4a38-bd5e-5714b9ec7efa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# Superposiciones de vídeo y HTML de fase{#stagevideo-and-html-overlays}

Puede utilizar las superposiciones de HTML con StageVideo para mostrar los elementos de la interfaz de usuario en el plano de vídeo de la lista de visualización de Flash. Este plano está por encima del plano de StageVideo, por lo que StageVideo siempre se muestra detrás de los elementos de la lista de visualización de Flash.

Las superposiciones de HTML son elementos de la interfaz de usuario que se pueden mostrar en el plano de visualización del Flash en un vídeo procesado por `StageVideo` en su propio avión. Antes del Flash 15, no se podían usar superposiciones de HTML cuando la aceleración de hardware no estaba disponible. A partir del Flash 15, las superposiciones de HTML se muestran cuando `StageVideo` vuelve a la renderización por software.

>[!IMPORTANT]
>
>Según las capacidades del sistema, el rendimiento puede reducirse en bueno o en menor grado al utilizar superposiciones de HTML.

Tenga en cuenta la siguiente información:

* En el Flash Player 15:

   * Puede utilizar superposiciones de HTML si la aceleración de hardware está disponible.
   * Para usar superposiciones de HTML, establezca `wmode` hasta `opaque`.

* En el Flash Player 14:

   * Cuando la aceleración de hardware está disponible, `StageVideo` reside debajo de la lista de visualización de Flash, por lo que puede utilizar superposiciones de HTML.
   * Cuando la aceleración de hardware no está disponible, el vídeo se procesa sobre todos los demás elementos del explorador, lo que impide el uso de superposiciones de HTML.

Estos son los requisitos mínimos del explorador para utilizar superposiciones de HTML con `StageVideo`:

* Firefox versión 4 y posterior
* Safari versión 4 y posterior
* Internet Explorer:

   * Versión 9+ en Windows 7 y posterior
   * Versión 10+ en Windows XP

* Chrome versión 26 y posterior

   >[!IMPORTANT]
   >
   >Chrome Pepper en Windows XP y Windows Vista no es compatible.
