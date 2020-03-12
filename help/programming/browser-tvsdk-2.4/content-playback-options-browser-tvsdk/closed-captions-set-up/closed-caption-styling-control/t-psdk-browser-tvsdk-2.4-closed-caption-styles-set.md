---
description: Puede definir el formato, como la fuente, el tamaño, el color, el borde y la opacidad del texto de subtítulos opcionales.
seo-description: Puede definir el formato, como la fuente, el tamaño, el color, el borde y la opacidad del texto de subtítulos opcionales.
seo-title: Definición de estilos de subtítulos opcionales
title: Definición de estilos de subtítulos opcionales
uuid: 906ed22c-e673-4211-a14b-d95d176aad21
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Definición de estilos de subtítulos opcionales{#set-closed-caption-styles}

Puede definir el formato, como la fuente, el tamaño, el color, el borde y la opacidad del texto de subtítulos opcionales.

1. Espere a que el `MediaPlayer` estado esté al menos en el estado PREPARADO.

   Para obtener más información sobre los estados, consulte [Esperar un estado](../../../content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-state-prepared-wait-for.md)válido.
1. Cree una `TextFormat` instancia.

   Puede proporcionar todos los parámetros de estilo de subtítulos opcionales ahora o establecerlos más tarde.

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

1. (Opcional) Obtenga la configuración actual del estilo de subtítulos opcionales con `MediaPlayer.ccStyle`.

   El valor devuelto es una instancia de la `TextFormat` interfaz.

   Si no se estableció ningún estilo anteriormente, devuelve un objeto TextFormat con valores predeterminados para cada atributo:

   ```js
   ccStyle :AdobePSDK.TextFormat
   ```

1. Para cambiar la configuración de estilo, utilice `MediaPlayer.ccStyle`, pasando una instancia de la `TextFormat` interfaz.

   Puede utilizar este método aunque el flujo de medios actual no tenga subtítulos opcionales.

   ```js
   ccStyle :AdobePSDK.TextFormat 
   ```

   >[!TIP]
   >
   >La configuración del estilo de subtítulos opcionales es asincrónica, por lo que los cambios pueden tardar unos segundos en aparecer en la pantalla.

