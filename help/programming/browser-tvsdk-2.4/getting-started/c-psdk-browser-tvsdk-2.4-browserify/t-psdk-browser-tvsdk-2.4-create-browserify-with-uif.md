---
description: Utilice los archivos de biblioteca Browserify proporcionados por el SDK de TVSDK del explorador en la aplicación para crear un reproductor compatible con Browserify mediante la interfaz de usuario del marco.
title: Creación de un reproductor compatible con Browserify mediante la interfaz de usuario del marco
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# Cree un reproductor compatible con Browserify utilizando la interfaz de usuario del marco {#create-a-browserify-compatible-player-using-the-ui-framework}

Utilice los archivos de biblioteca Browserify proporcionados por el SDK de TVSDK del explorador en la aplicación para crear un reproductor compatible con Browserify mediante la interfaz de usuario del marco.

Archivos Browserify de ejemplo incluidos en el TVSDK:

* [!DNL [..]/samples/browserify/ui-framework/build/Gruntfile.js]
* [!DNL [..]/samples/browserify/ui-framework/build/package.json]
* [!DNL [..]/samples/browserify/ui-framework/examples/sample.html]
* [!DNL [..]/samples/browserify/ui-framework/examples/sample.js]

Para crear una aplicación compatible con Browserify mediante el marco de IU, debe `require` usar los dos módulos Browserify (proporcionados por el TVSDK del explorador) en el código de la aplicación:

1. Requerir módulos Browserify:

   ```
   var AdobePSDK = require('../../../../frameworks/player/AdobePSDK.module.js');  
   var ptp = require('../../../ui-framework/libs/Primetimevisualapi.module.js);  
   […]
   ```

1. Continúe con el desarrollo descrito en [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-uif.md).
>Ahora puede empaquetar los archivos de la aplicación mediante Browserify.
