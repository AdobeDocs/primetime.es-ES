---
description: Para utilizar los apariencias personalizadas, debe escribir la personalización similar a default-video-Controls.css y hacer referencia a esta nueva personalización en el reproductor.
seo-description: Para utilizar los apariencias personalizadas, debe escribir la personalización similar a default-video-Controls.css y hacer referencia a esta nueva personalización en el reproductor.
seo-title: Pieles personalizadas
title: Pieles personalizadas
uuid: bc71926e-0dec-4628-8248-911224a7a6c2
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Pieles personalizadas{#custom-skins}

Para utilizar los apariencias personalizadas, debe escribir la personalización similar a default-video-Controls.css y hacer referencia a esta nueva personalización en el reproductor.

Por ejemplo, puede utilizar una de las siguientes opciones:

* `<link rel="stylesheet" href="css/common_style.css">`
* `<link rel="stylesheet" href="css/custom-video-controls1.css">`

Puede realizar los siguientes tipos de cambios:

* Color frontal de botones y texto

   Todos los controles que tienen un primer plano utilizan la `vid-skin-fgcolor` clase. Para cambiar el primer plano de todos los controles, repita todos los elementos con la `vid-skin-fgcolor` clase y especifique el color deseado.
* Color de fondo de botones y texto

   Todos los controles que tienen un primer plano utilizan la `vid-skin-bgcolor` clase. Para cambiar el primer plano de todos los controles, repita todos los elementos con `vid-skin-bgcolor` clase y especifique el color deseado.
* Forma del cabezal de reproducción

   El cursor de reproducción puede ser cuadrado o redondo. Para cambiar el cursor de reproducción, agregue `square` o `round` clase al `playhead` elemento.
* Estilo de los spinners de almacenamiento en búfer

   El reproductor de referencia proporciona los siguientes estilos de spinners que se pueden mostrar a medida que el reproductor almacena en búfer el contenido:

   * Texto superpuesto ( `overlay-text`)
   * Girador rectangular ( `spinner`)
   * Señal ( `signal`)
   * Barras verticales ( `vertical`)

      >[!TIP]
      >
      >Para utilizar cualquiera de los spinners en búfer, debe agregar la clase en el elemento buffering-overlay. Por ejemplo, para usar `overlay-text`, agregue las siguientes líneas en el `BufferOverlay.js` archivo:
      >
      >
      ```js
      >var overlay = document.getElementById("buffering-overlay"); 
      >overlay.classList.add ("spinner");
      >```

