---
description: Para utilizar las máscaras personalizadas, debe escribir la personalización de forma similar a default-video-controls.css y hacer referencia a esta nueva personalización en el reproductor.
title: Apariencias personalizadas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---

# Apariencias personalizadas{#custom-skins}

Para utilizar las máscaras personalizadas, debe escribir la personalización de forma similar a default-video-controls.css y hacer referencia a esta nueva personalización en el reproductor.

Por ejemplo, puede utilizar una de las siguientes opciones:

* `<link rel="stylesheet" href="css/common_style.css">`
* `<link rel="stylesheet" href="css/custom-video-controls1.css">`

Puede realizar los siguientes tipos de cambios:

* Color de primer plano de los botones y el texto

  Todos los controles que tienen un primer plano utilizan el `vid-skin-fgcolor` clase. Para cambiar el primer plano de todos los controles, recorra en iteración todos los elementos con el `vid-skin-fgcolor` y especifique el color que desee.
* Color de fondo de los botones y el texto

  Todos los controles que tienen un primer plano utilizan el `vid-skin-bgcolor` clase. Para cambiar el primer plano de todos los controles, recorra en iteración todos los elementos con `vid-skin-bgcolor` y especifique el color que desee.
* Forma del cabezal de reproducción

  El cabezal de reproducción puede ser cuadrado o redondo. Para cambiar el cabezal de reproducción, añada `square` o `round` clase a `playhead` Elemento.
* Estilo de los hiladores de almacenamiento en búfer

  El reproductor de referencia proporciona los siguientes estilos de giros que se pueden mostrar como contenido de búfer del reproductor:

   * Overlay-text ( `overlay-text`)
   * Girador rectangular ( `spinner`)
   * Señal ( `signal`)
   * Barras verticales ( `vertical`)

     >[!TIP]
     >
     >Para utilizar cualquiera de los giros de almacenamiento en búfer, debe agregar la clase en el elemento buffering-overlay. Por ejemplo, para utilizar `overlay-text`, agregue las siguientes líneas en la `BufferOverlay.js` archivo:
     >
     >```js
     >var overlay = document.getElementById("buffering-overlay"); 
     >overlay.classList.add ("spinner");
     >```
     >
