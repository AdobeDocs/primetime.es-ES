---
description: Puede utilizar superposiciones HTML con StageVideo para mostrar elementos de IU en el plano de vídeo de la lista de visualización de Flash. Este plano está por encima del plano StageVideo, por lo que StageVideo siempre se muestra detrás de cualquier elemento de lista de visualización de Flash.
title: Superposiciones de StageVideo y HTML
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---


# Superposiciones de StageVideo y HTML{#stagevideo-and-html-overlays}

Puede utilizar superposiciones HTML con StageVideo para mostrar elementos de IU en el plano de vídeo de la lista de visualización de Flash. Este plano está por encima del plano StageVideo, por lo que StageVideo siempre se muestra detrás de cualquier elemento de lista de visualización de Flash.

Las superposiciones HTML son elementos de la interfaz de usuario que se pueden mostrar en el plano de visualización del Flash en vídeo procesado por `StageVideo` en su propio plano. Antes del Flash 15, no se podían usar superposiciones HTML cuando la aceleración de hardware no estaba disponible. A partir del Flash 15, las superposiciones HTML se muestran cuando `StageVideo` vuelve a la representación de software.

>[!IMPORTANT]
>
>Según las capacidades del sistema, el rendimiento puede degradarse a un bueno o menor grado al utilizar superposiciones HTML.

Tenga en cuenta la siguiente información:

* En el Flash Player 15:

   * Puede utilizar las superposiciones HTML si la aceleración de hardware está disponible.
   * Para utilizar superposiciones HTML, establezca `wmode` en `opaque`.

* En el Flash Player 14:

   * Cuando la aceleración de hardware está disponible, `StageVideo` reside debajo de la lista de visualización de Flash, por lo que puede utilizar las superposiciones HTML.
   * Cuando la aceleración de hardware no está disponible, el vídeo se procesa sobre todos los demás elementos del navegador, lo que impide el uso de superposiciones HTML.

Estos son los requisitos mínimos del explorador para utilizar las superposiciones HTML con `StageVideo`:

* Firefox versión 4 y posterior
* Safari versión 4 y posterior
* Internet Explorer:

   * Versión 9+ en Windows 7 y posterior
   * Versión 10+ en Windows XP

* Chrome versión 26 y posteriores

   >[!IMPORTANT]
   >
   >Chrome Pepper en Windows XP y Windows Vista no es compatible.

