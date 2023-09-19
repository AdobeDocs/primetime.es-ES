---
description: Puede mostrar subtítulos al reproducir contenido de vídeo.
title: Subtítulos
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '55'
ht-degree: 0%

---

# Subtítulos{#captions}

Puede mostrar subtítulos al reproducir contenido de vídeo.

Para gestionar subtítulos, debe añadir la variable `AdobePSDK.PSDKEventType.CAPTIONS_UPDATED` detector de eventos:

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

El marco de trabajo de la interfaz de usuario proporciona una implementación de comportamientos de subtítulos predeterminada que se puede modificar. Los comportamientos de subtítulos cerrados también se pueden modificar ampliando los comportamientos de subtítulos cerrados predeterminados. Por ejemplo:

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
