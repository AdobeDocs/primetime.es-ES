---
description: Utilice los archivos de biblioteca Browserify proporcionados por el TVSDK del explorador en la aplicación para crear un reproductor compatible con Browserify mediante el marco de interfaz de usuario.
title: Creación de un reproductor compatible con Browserify mediante el marco de interfaz de usuario
exl-id: cd72cae1-f67e-4192-9a7e-1c1492d88922
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---

# Creación de un reproductor compatible con Browserify mediante el marco de interfaz de usuario {#create-a-browserify-compatible-player-using-the-ui-framework}

Utilice los archivos de biblioteca Browserify proporcionados por el TVSDK del explorador en la aplicación para crear un reproductor compatible con Browserify mediante el marco de interfaz de usuario.

Archivos Browserify de muestra incluidos en el TVSDK:

* [!DNL [...]/samples/browserify/ui-framework/build/Gruntfile.js]
* [!DNL [...]/samples/browserify/ui-framework/build/package.json]
* [!DNL [...]/samples/browserify/ui-framework/examples/sample.html]
* [!DNL [...]/samples/browserify/ui-framework/examples/sample.js]

Para crear una aplicación compatible con Browserify mediante UI-Framework, debe `require` Utilice los dos módulos Browserify (proporcionados por Browser TVSDK) en el código de la aplicación:

1. Requerir módulos Browserify:

   ```
   var AdobePSDK = require('../../../../frameworks/player/AdobePSDK.module.js');  
   var ptp = require('../../../ui-framework/libs/Primetimevisualapi.module.js);  
   […]
   ```

1. Continúe con el desarrollo como se describe en [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-uif.md).
>Ahora puede empaquetar los archivos de la aplicación mediante Browserify.
