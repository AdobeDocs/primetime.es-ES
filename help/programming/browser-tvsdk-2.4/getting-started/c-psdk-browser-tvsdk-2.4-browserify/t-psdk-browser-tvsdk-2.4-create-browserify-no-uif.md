---
description: Utilice el archivo de biblioteca Browserify proporcionado por el SDK de TVSDK del explorador en la aplicación para crear un reproductor compatible con Browserify.
title: Creación de un reproductor compatible con Browserify sin la interfaz de usuario del marco
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---


# Crear un reproductor compatible con Browserify sin la interfaz de usuario-Framework{#create-a-browserify-compatible-player-without-the-ui-framework}

Utilice el archivo de biblioteca Browserify proporcionado por el SDK de TVSDK del explorador en la aplicación para crear un reproductor compatible con Browserify.

El tema [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md) enumera el conjunto de bibliotecas TVSDK del explorador que se incluyen normalmente al crear un reproductor de vídeo básico. Para ello, simplemente agregue etiquetas `script` con atributos `src` que apunten a las bibliotecas.

El proceso es ligeramente diferente para crear un reproductor compatible con Browserify. Para ello, utilice el comando `require` para incluir el archivo [!DNL AdobePSDK.module.js] (proporcionado por el TVSDK del explorador) en la aplicación. Este archivo agrupa los archivos básicos de la biblioteca del reproductor en el orden adecuado de dependencia y devuelve el `AdobePSDK` espacio de nombres que utiliza para implementar características para el reproductor.

El TVSDK del explorador proporciona el siguiente ejemplo de aplicación Browserify y archivos de compilación en el paquete de versión:

* [!DNL [..]/samples/browserify/reference/build/Gruntfile.js]
* [!DNL [..]/samples/browserify/reference/build/package.json]
* [!DNL [..]/samples/browserify/reference/examples/sample.html]
* [!DNL [..]/samples/browserify/reference/examples/sample.js]

Para crear un reproductor de vídeo compatible con Browserify:

1. Requerir el archivo de biblioteca compatible con Browserify que devuelve el espacio de nombres `AdobePSDK`:

   ```
   var AdobePSDK = require('./AdobePSDK.module.js'); 
   var player; 
   function Load () { 
       player = new AdobePSDK.MediaPlayer(); 
   […]
   ```

1. Cree el reproductor como se describe en [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md).

   El paso 1 de esta tarea reemplaza el paso de las instrucciones básicas del reproductor en el que se originan las bibliotecas básicas individuales del reproductor en el archivo de la aplicación.
Ahora puede empaquetar los archivos de la aplicación mediante Browserify.
