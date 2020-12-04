---
description: Utilice el archivo de biblioteca Browserify proporcionado por el SDK de TVSDK del explorador en la aplicación para crear un reproductor compatible con Browserify.
seo-description: Utilice el archivo de biblioteca Browserify proporcionado por el SDK de TVSDK del explorador en la aplicación para crear un reproductor compatible con Browserify.
seo-title: Creación de un reproductor compatible con Browserify sin interfaz de usuario-marco
title: Creación de un reproductor compatible con Browserify sin interfaz de usuario-marco
uuid: c4315bc8-c75d-4dd9-8680-946c1197be1e
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---


# Crear un reproductor compatible con Browserify sin UI-Framework{#create-a-browserify-compatible-player-without-the-ui-framework}

Utilice el archivo de biblioteca Browserify proporcionado por el SDK de TVSDK del explorador en la aplicación para crear un reproductor compatible con Browserify.

El tema [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md) lista el conjunto de bibliotecas TVSDK del explorador que normalmente se incluye al crear un reproductor de vídeo básico. Para ello, simplemente agregue etiquetas `script` con atributos `src` que apunten a las bibliotecas.

El proceso es ligeramente diferente para crear un reproductor compatible con Browserify. Para ello, utilice el comando `require` para incluir el archivo [!DNL AdobePSDK.module.js] (proporcionado por el TVSDK del explorador) en la aplicación. Este archivo agrupa los archivos de biblioteca básicos del reproductor en el orden de dependencia adecuado y devuelve la Área de nombres `AdobePSDK` que utiliza para implementar las funciones del reproductor.

El SDK de TVSDK del explorador proporciona el siguiente ejemplo de aplicación de exploración y compilación de archivos en el paquete de versión:

* [!DNL [...]/samples/browserify/reference/build/Gruntfile.js]
* [!DNL [...]/samples/browserify/reference/build/package.json]
* [!DNL [...]/samples/browserify/reference/examples/sample.html]
* [!DNL [...]/samples/browserify/reference/examples/sample.js]

Para crear un reproductor de vídeo compatible con Browserify:

1. Requerir el archivo de biblioteca compatible con Browserify que devuelve la Área de nombres `AdobePSDK`:

   ```
   var AdobePSDK = require('./AdobePSDK.module.js'); 
   var player; 
   function Load () { 
       player = new AdobePSDK.MediaPlayer(); 
   […]
   ```

1. Cree el reproductor como se describe en [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md).

   El paso 1 de esta tarea sustituye al paso de las instrucciones básicas del reproductor en el que se originan las bibliotecas de reproductor básicas individuales en el archivo de la aplicación.
Ahora puede compilar los archivos de la aplicación mediante Browserify.
