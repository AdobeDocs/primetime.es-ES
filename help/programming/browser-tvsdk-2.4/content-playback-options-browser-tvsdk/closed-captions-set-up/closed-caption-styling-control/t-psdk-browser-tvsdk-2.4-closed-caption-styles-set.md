---
description: Puede definir el formato, como la fuente, el tamaño, el color, el borde y la opacidad del texto de subtítulos.
title: Definir estilos de subtítulos
exl-id: 7ece68ce-0dc5-4899-9834-39940bbd0332
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 0%

---

# Definir estilos de subtítulos{#set-closed-caption-styles}

Puede definir el formato, como la fuente, el tamaño, el color, el borde y la opacidad del texto de subtítulos.

1. Espere a que `MediaPlayer` para que esté al menos en estado PREPARADO.

   Para obtener más información sobre los estados, consulte [Esperar a un estado válido](../../../content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-state-prepared-wait-for.md).
1. Crear un `TextFormat` ejemplo.

   Puede proporcionar todos los parámetros de estilo de subtítulos ahora o establecerlos más adelante.

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

1. (Opcional) Obtenga la configuración actual del estilo de subtítulos con `MediaPlayer.ccStyle`.

   El valor devuelto es una instancia de `TextFormat` interfaz.

   Si no se estableció ningún estilo anteriormente, devuelve un objeto TextFormat con valores predeterminados para cada atributo:

   ```js
   ccStyle :AdobePSDK.TextFormat
   ```

1. Para cambiar la configuración de estilo, utilice `MediaPlayer.ccStyle`, pasando una instancia de `TextFormat` interfaz.

   Puede utilizar este método incluso si el flujo de medios actual no tiene subtítulos.

   ```js
   ccStyle :AdobePSDK.TextFormat 
   ```

   >[!TIP]
   >
   >La configuración del estilo de subtítulos opcionales es asíncrona, por lo que los cambios pueden tardar unos segundos en aparecer en la pantalla.
