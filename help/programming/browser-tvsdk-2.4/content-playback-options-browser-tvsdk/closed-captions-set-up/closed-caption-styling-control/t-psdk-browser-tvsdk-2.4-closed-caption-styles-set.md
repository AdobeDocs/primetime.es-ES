---
description: Puede definir el formato, como la fuente, el tamaño, el color, el borde y la opacidad del texto de subtítulos.
title: Definición de estilos de subtítulos
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---


# Establecer estilos de subtítulos {#set-closed-caption-styles}

Puede definir el formato, como la fuente, el tamaño, el color, el borde y la opacidad del texto de subtítulos.

1. Espere a que `MediaPlayer` esté al menos en el estado PREPARADO.

   Para obtener más información sobre los estados, consulte [Espera a un estado válido](../../../content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-state-prepared-wait-for.md).
1. Cree una instancia `TextFormat`.

   Ahora puede proporcionar todos los parámetros de estilo de subtítulos o definirlos más adelante.

   ```js
   new TextFormat( 
       font,   
       fontColor,  
       edgeColor,   
       fontEdge,  
       backgroundColor,   
       fillColor,  
       size,   
       fontOpacity,   
       backgroundOpacity,  
       fillOpacity, 
       bottomInset 
       safeArea) → {AdobePSDK.TextFormat}
   ```

1. (Opcional) Obtenga la configuración actual de estilo de subtítulos con `MediaPlayer.ccStyle`.

   El valor devuelto es una instancia de la interfaz `TextFormat`.

   Si no se estableció ningún estilo anteriormente, devuelve un objeto TextFormat con valores predeterminados para cada atributo:

   ```js
   ccStyle :AdobePSDK.TextFormat
   ```

1. Para cambiar la configuración de estilo, utilice `MediaPlayer.ccStyle` y pase una instancia de la interfaz `TextFormat`.

   Puede utilizar este método aunque el flujo de medios actual no tenga subtítulos.

   ```js
   ccStyle :AdobePSDK.TextFormat 
   ```

   >[!TIP]
   >
   >La configuración del estilo de subtítulos es asíncrona, por lo que los cambios podrían tardar unos segundos en aparecer en la pantalla.

