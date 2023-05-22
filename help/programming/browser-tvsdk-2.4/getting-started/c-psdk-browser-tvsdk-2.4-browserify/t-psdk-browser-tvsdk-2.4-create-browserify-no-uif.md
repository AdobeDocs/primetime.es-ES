---
description: Utilice el archivo de biblioteca Browserify proporcionado por el TVSDK del explorador en la aplicación para crear un reproductor compatible con Browserify.
title: Crear un reproductor compatible con Browserify sin UI-Framework
exl-id: 27b5e1c5-49c3-44e4-9e34-0f50a50e36f5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Crear un reproductor compatible con Browserify sin UI-Framework{#create-a-browserify-compatible-player-without-the-ui-framework}

Utilice el archivo de biblioteca Browserify proporcionado por el TVSDK del explorador en la aplicación para crear un reproductor compatible con Browserify.

El tema [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md) muestra el conjunto de bibliotecas de TVSDK del explorador que suele incluir al crear un reproductor de vídeo básico. Para ello, simplemente añada `script` etiquetas con `src` atributos que apuntan a las bibliotecas.

El proceso es ligeramente diferente para crear un reproductor compatible con Browserify. Para ello, utilice el `require` para incluir el [!DNL AdobePSDK.module.js] (proporcionado por el TVSDK del explorador) en la aplicación. Este archivo agrupa los archivos de la biblioteca del reproductor básico en el orden adecuado de dependencia y devuelve el valor `AdobePSDK` área de nombres que se utiliza para implementar funciones para el reproductor.

Browser TVSDK proporciona los siguientes archivos de ejemplo de la aplicación Browserify y los archivos de compilación en el paquete de la versión:

* [!DNL [...]/samples/browserify/reference/build/Gruntfile.js]
* [!DNL [...]/samples/browserify/reference/build/package.json]
* [!DNL [...]/samples/browserify/reference/examples/sample.html]
* [!DNL [...]/samples/browserify/reference/examples/sample.js]

Para crear un reproductor de vídeo compatible con Browserify:

1. Requiere el archivo de biblioteca compatible con Browserify que devuelve el `AdobePSDK` área de nombres:

   ```
   var AdobePSDK = require('./AdobePSDK.module.js'); 
   var player; 
   function Load () { 
       player = new AdobePSDK.MediaPlayer(); 
   […]
   ```

1. Cree su reproductor como se describe en [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md).

   El paso 1 de esta tarea reemplaza el paso en las instrucciones básicas del reproductor, en el que se obtienen las bibliotecas individuales básicas del reproductor en el archivo de la aplicación.
Ahora puede empaquetar los archivos de la aplicación mediante Browserify.
