---
description: Puede definir el formato, como la fuente, el tamaño, el color, el borde y la opacidad del texto de subtítulos opcionales.
seo-description: Puede definir el formato, como la fuente, el tamaño, el color, el borde y la opacidad del texto de subtítulos opcionales.
seo-title: Definición de estilos de subtítulos opcionales
title: Definición de estilos de subtítulos opcionales
uuid: 906ed22c-e673-4211-a14b-d95d176aad21
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---


# Establecer estilos de subtítulos opcionales{#set-closed-caption-styles}

Puede definir el formato, como la fuente, el tamaño, el color, el borde y la opacidad del texto de subtítulos opcionales.

1. Espere a que `MediaPlayer` esté al menos en el estado PREPARADO.

   Para obtener más información acerca de los estados, consulte [Esperar un estado válido](../../../content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-state-prepared-wait-for.md).
1. Cree una instancia `TextFormat`.

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

1. (Opcional) Obtenga la configuración de estilo de subtítulos opcionales actual con `MediaPlayer.ccStyle`.

   El valor devuelto es una instancia de la interfaz `TextFormat`.

   Si no se estableció ningún estilo anteriormente, devuelve un objeto TextFormat con valores predeterminados para cada atributo:

   ```js
   ccStyle :AdobePSDK.TextFormat
   ```

1. Para cambiar la configuración de estilo, utilice `MediaPlayer.ccStyle` y pase una instancia de la interfaz `TextFormat`.

   Puede utilizar este método aunque el flujo de medios actual no tenga subtítulos opcionales.

   ```js
   ccStyle :AdobePSDK.TextFormat 
   ```

   >[!TIP]
   >
   >La configuración del estilo de subtítulos opcionales es asincrónica, por lo que los cambios pueden tardar unos segundos en aparecer en la pantalla.

