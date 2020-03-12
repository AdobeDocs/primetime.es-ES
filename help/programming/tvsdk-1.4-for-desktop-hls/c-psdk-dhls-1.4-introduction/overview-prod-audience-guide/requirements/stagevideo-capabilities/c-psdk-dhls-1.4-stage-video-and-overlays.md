---
description: Puede utilizar las superposiciones HTML con StageVideo para mostrar los elementos de la interfaz de usuario en el plano de vídeo de la lista de visualización Flash. Este plano está por encima del plano de StageVideo, por lo que StageVideo siempre se muestra detrás de cualquier elemento de la lista de visualización Flash.
seo-description: Puede utilizar las superposiciones HTML con StageVideo para mostrar los elementos de la interfaz de usuario en el plano de vídeo de la lista de visualización Flash. Este plano está por encima del plano de StageVideo, por lo que StageVideo siempre se muestra detrás de cualquier elemento de la lista de visualización Flash.
seo-title: Superposiciones de StageVideo y HTML
title: Superposiciones de StageVideo y HTML
uuid: 84e862ab-4c35-47a2-9c4e-f792d3ef5363
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Superposiciones de StageVideo y HTML{#stagevideo-and-html-overlays}

Puede utilizar las superposiciones HTML con StageVideo para mostrar los elementos de la interfaz de usuario en el plano de vídeo de la lista de visualización Flash. Este plano está por encima del plano de StageVideo, por lo que StageVideo siempre se muestra detrás de cualquier elemento de la lista de visualización Flash.

Las superposiciones HTML son elementos de la interfaz de usuario que se pueden mostrar en el plano de visualización Flash en un vídeo que se procesa `StageVideo` en su propio plano. Antes de Flash 15, no se podían usar superposiciones HTML cuando no estaba disponible la aceleración de hardware. A partir de Flash 15, las superposiciones HTML se muestran cuando `StageVideo` regresan al procesamiento por software.

>[!IMPORTANT]
>
>Según las capacidades del sistema, el rendimiento puede degradarse en bueno o en menor grado al utilizar superposiciones HTML.

Considere la siguiente información:

* En Flash Player 15:

   * Puede utilizar las superposiciones HTML si está disponible la aceleración de hardware.
   * Para utilizar superposiciones HTML, defina `wmode` en `opaque`.

* En Flash Player 14:

   * Cuando la aceleración de hardware está disponible, `StageVideo` reside debajo de la lista de visualización de Flash, para que pueda utilizar las superposiciones HTML.
   * Cuando la aceleración de hardware no está disponible, el vídeo se procesa sobre todos los demás elementos del navegador, lo que impide el uso de superposiciones HTML.

Estos son los requisitos mínimos del explorador para utilizar superposiciones HTML con `StageVideo`:

* Firefox versión 4 y posterior
* Safari versión 4 y posterior
* Internet Explorer:

   * Versión 9+ en Windows 7 y posterior
   * Versión 10+ en Windows XP

* Chrome versión 26 y posterior

   >[!IMPORTANT]
   >
   >Chrome Pepper en Windows XP y Windows Vista no es compatible.

