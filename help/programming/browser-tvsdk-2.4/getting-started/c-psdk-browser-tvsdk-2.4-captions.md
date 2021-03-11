---
description: Los subtítulos se pueden mostrar al reproducir contenido de vídeo.
title: Subtítulos
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '55'
ht-degree: 3%

---


# Subtítulos{#captions}

Los subtítulos se pueden mostrar al reproducir contenido de vídeo.

Para gestionar los rótulos, debe añadir el detector de eventos `AdobePSDK.PSDKEventType.CAPTIONS_UPDATED`:

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

El marco de la interfaz de usuario proporciona una implementación de comportamientos de subtítulos predeterminada, que se puede modificar. Los comportamientos de los subtítulos también se pueden modificar ampliando los comportamientos predeterminados de los subtítulos. Por ejemplo:

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
