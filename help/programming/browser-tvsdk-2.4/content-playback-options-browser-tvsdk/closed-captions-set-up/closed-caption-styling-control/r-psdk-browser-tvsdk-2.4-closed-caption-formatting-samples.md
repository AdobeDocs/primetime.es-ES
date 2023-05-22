---
description: Puede especificar el formato de subtítulos.
title: Ejemplos Formato de rótulo
exl-id: 946530a1-c7d7-4582-81b8-71b2980561cb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '33'
ht-degree: 0%

---

# Ejemplos: Caption formatting{#examples-caption-formatting}

Puede especificar el formato de subtítulos.

## Ejemplo 1: Especificar valores de formato explícitamente {#section_BD7B48F3B66D4E9290E1CB2F464E08E4}

```js
// Set CC style. 
var tf = new AdobePSDK.TextFormat( 
      AdobePSDK.TextFormat.FONT_DEFAULT, 
      AdobePSDK.TextFormat.COLOR_DEFAULT, 
      AdobePSDK.TextFormat.COLOR_DEFAULT, 
      AdobePSDK.TextFormat.FONT_EDGE_DEFAULT, 
      AdobePSDK.TextFormat.COLOR_DEFAULT, 
      AdobePSDK.TextFormat.COLOR_DEFAULT, 
      AdobePSDK.TextFormat.SIZE_DEFAULT, 
      AdobePSDK.TextFormat.DEFAULT_OPACITY, 
      AdobePSDK.TextFormat.DEFAULT_OPACITY, 
      AdobePSDK.TextFormat.DEFAULT_OPACITY; 
 mediaPlayer.CCStyle(tf);
```

>[!IMPORTANT]
>
>El TVSDK del explorador no admite bordes de fuentes, colores de relleno u opacidad de relleno.
