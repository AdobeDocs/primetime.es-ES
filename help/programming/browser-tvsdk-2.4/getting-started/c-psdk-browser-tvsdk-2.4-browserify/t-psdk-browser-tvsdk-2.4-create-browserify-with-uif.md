---
description: Utilice los archivos de biblioteca Browserify proporcionados por el SDK de TVSDK del explorador en la aplicación para crear un reproductor compatible con Browserify mediante la interfaz de usuario y el marco de trabajo.
seo-description: Utilice los archivos de biblioteca Browserify proporcionados por el SDK de TVSDK del explorador en la aplicación para crear un reproductor compatible con Browserify mediante la interfaz de usuario y el marco de trabajo.
seo-title: Creación de un reproductor compatible con Browserify mediante la interfaz de usuario y el marco de trabajo
title: Creación de un reproductor compatible con Browserify mediante la interfaz de usuario y el marco de trabajo
uuid: 544fd872-5ca1-417d-8aab-69613caada0e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# Crear un reproductor compatible con Browserify mediante la interfaz de usuario-Framework {#create-a-browserify-compatible-player-using-the-ui-framework}

Utilice los archivos de biblioteca Browserify proporcionados por el SDK de TVSDK del explorador en la aplicación para crear un reproductor compatible con Browserify mediante la interfaz de usuario y el marco de trabajo.

Archivos de exploración de muestra incluidos en el TVSDK:

* [!DNL [...]/samples/browserify/ui-framework/build/Gruntfile.js]
* [!DNL [...]/samples/browserify/ui-framework/build/package.json]
* [!DNL [...]/samples/browserify/ui-framework/examples/sample.html]
* [!DNL [...]/samples/browserify/ui-framework/examples/sample.js]

Para crear una aplicación compatible con Browserify mediante la interfaz de usuario del marco, debe `require` los dos módulos de Browserify (proporcionados por el TVSDK del explorador) en el código de la aplicación:

1. Requerir módulos de Browserify:

   ```
   var AdobePSDK = require('../../../../frameworks/player/AdobePSDK.module.js');  
   var ptp = require('../../../ui-framework/libs/Primetimevisualapi.module.js);  
   […]
   ```

1. Continúe con el desarrollo descrito en [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-uif.md).
>Ahora puede compilar los archivos de la aplicación mediante Browserify.
