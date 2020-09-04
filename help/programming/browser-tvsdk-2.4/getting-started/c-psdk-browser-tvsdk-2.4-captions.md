---
description: Puede mostrar subtítulos al reproducir contenido de vídeo.
seo-description: Puede mostrar subtítulos al reproducir contenido de vídeo.
seo-title: Rótulos
title: Rótulos
uuid: 4dedcedc-50e5-4983-bb09-3f316337117e
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 3%

---


# Rótulos{#captions}

Puede mostrar subtítulos al reproducir contenido de vídeo.

Para gestionar rótulos, debe agregar el detector de `AdobePSDK.PSDKEventType.CAPTIONS_UPDATED` eventos:

```js
... 
player.addEventListener(AdobePSDK.PSDKEventType.CAPTIONS_UPDATED,  
                        onCaptionsUpdateEvent); 
... 
function onCaptionsUpdateEvent (event) { 
  // code to show the captions icon and any settings button. 
<pre>
   For example: 
  var btnCC = document.getElementById("btn_captions"); 
   btnCC.classList.remove("invisible"); 
   
  var btnSettings = document.getElementById("btn_settings"); 
   btnSettings.classList.remove("invisible"); 
 } 
</pre>
```

El marco de interfaz de usuario proporciona una implementación de comportamientos de subtítulos predeterminados, que se puede modificar. Los comportamientos de los subtítulos opcionales también se pueden modificar ampliando los comportamientos de los subtítulos opcionales predeterminados. Por ejemplo:

```js
// Using UI Framework 
var playerWrapper = ptp.videoPlayer(‘.videoDiv', { 
player:{ 
    mediaResource: 'Specify Resource URL', 
    ccStyle: { 
    font:AdobePSDK.TextFormat.CURSIVE, 
    fontColor:AdobePSDK.TextFormat.BRIGHT_WHITE, 
    edgeColor:AdobePSDK.TextFormat.BLUE, 
    backgroundColor:AdobePSDK.TextFormat.BLACK, 
    fillColor:AdobePSDK.TextFormat.BLUE, 
    size:AdobePSDK.TextFormat.MEDIUM, 
    fontOpacity:100, 
    backgroundOpacity:1, 
    fillOpacity:1 
   } 
 } 
 
}); 
```
