---
description: Para utilizar los aspectos personalizados, debe escribir la personalización similar a default-video-controls.css y hacer referencia a esta nueva personalización en el reproductor.
title: Pieles personalizadas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '218'
ht-degree: 0%

---


# Pieles personalizadas{#custom-skins}

Para utilizar los aspectos personalizados, debe escribir la personalización similar a default-video-controls.css y hacer referencia a esta nueva personalización en el reproductor.

Por ejemplo, puede utilizar una de las siguientes opciones:

* `<link rel="stylesheet" href="css/common_style.css">`
* `<link rel="stylesheet" href="css/custom-video-controls1.css">`

Puede realizar los siguientes tipos de cambios:

* Color de primer plano de botones y texto

   Todos los controles que tienen un primer plano utilizan la clase `vid-skin-fgcolor`. Para cambiar el primer plano de todos los controles, repita todos los elementos con la clase `vid-skin-fgcolor` y especifique el color deseado.
* Color de fondo de botones y texto

   Todos los controles que tienen un primer plano utilizan la clase `vid-skin-bgcolor`. Para cambiar el primer plano de todos los controles, repita todos los elementos con la clase `vid-skin-bgcolor` y especifique el color deseado.
* Forma del cabezal de reproducción

   El cabezal de reproducción puede ser cuadrado o redondo. Para cambiar el cabezal de reproducción, agregue la clase `square` o `round` al elemento `playhead`.
* Estilo de los giros de almacenamiento en búfer

   El reproductor de referencia proporciona los siguientes estilos de giros que se pueden mostrar cuando el reproductor almacena en el búfer el contenido:

   * Texto de superposición ( `overlay-text`)
   * Girador rectangular ( `spinner`)
   * Señal ( `signal`)
   * Barras verticales ( `vertical`)

      >[!TIP]
      >
      >Para utilizar cualquiera de los giros de almacenamiento en búfer, debe añadir la clase en el elemento de almacenamiento en búfer y superposición. Por ejemplo, para utilizar `overlay-text`, agregue las siguientes líneas en el archivo `BufferOverlay.js`:
      >
      >
      ```js
      >var overlay = document.getElementById("buffering-overlay"); 
      >overlay.classList.add ("spinner");
      >```

