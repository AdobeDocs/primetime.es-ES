---
title: Añadir publicidad
description: Añadir publicidad
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '49'
ht-degree: 0%

---


# Agregar publicidad {#add-advertising}

1. Defina los metadatos publicitarios.

   ```js
   var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
     auditudeSettings.domain = "auditude.com"; 
     auditudeSettings.mediaId = "adbe_tearsofsteel2"; 
     auditudeSettings.zoneId = "123869";
   ```

1. Agregue los metadatos publicitarios a `MediaResource`.

   ```js
   var mediaResource =  
     new AdobePSDK.MediaResource(resourceUrl, resourceType, auditudeSettings, false);
   ```

1. Agregue la configuración a la configuración y agregue una fábrica de analizador `SpliceOut`.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings; 
   config.advertisingFactory = new ExtCueOutContentFactory(auditudeSettings);
   ```

1. Agregue `ExtCueOutContentFactory` a la sección de la biblioteca.
1. Descargue el `ExtCueOutContentFactory.js` de la sección de la biblioteca y colóquelo en la carpeta de trabajo.

   ```js
   <script src= "frameworks/player/dash.min.js"></script> 
   <script src= "frameworks/player/primetimemain.min.js"></script> 
   <script src= "frameworks/player/swfobject.js"></script> 
   <script src= "frameworks/player/primetimeei.min.js"></script> 
   <script src= "ExtCueOutContentFactory.js"></script>
   ```

1. Pruebe la configuración.
