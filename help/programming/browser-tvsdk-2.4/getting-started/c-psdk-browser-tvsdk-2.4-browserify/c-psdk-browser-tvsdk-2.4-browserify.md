---
description: Puede crear un reproductor compatible con Browserify utilizando los archivos JS proporcionados por el TVSDK del explorador.
title: Reproductor compatible con Browserify
exl-id: 3e9751d8-7a7e-465b-8d46-d07e4ccb1f5b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---

# Información general {#browserify-compatible-player-overview}

Puede crear un reproductor compatible con Browserify utilizando los archivos JS proporcionados por el TVSDK del explorador.

El TVSDK del explorador proporciona dos archivos JS compatibles con Browserify. Una es para usar con el módulo AdobePSDK; esta es para desarrollar aplicaciones sin UI-Framework. El otro es para usar con el módulo UI-Framework; devuelve el espacio de nombres PTP que usa para escribir aplicaciones mediante UI-Framework.

Para empezar a usar Browserify, ejecute los siguientes comandos de configuración para crear [!DNL final.js] archivos (el archivo del paquete Browserify) dentro de [!DNL example] directorios bajo [!DNL samples/browerify/reference] y [!DNL samples/browerify/ui-framework]:

1. Vaya a [!DNL samples/browserify/reference/build].
1. Ejecute los siguientes comandos:

   1. [!DNL npm install]
   1. [!DNL node_modules/.bin/grunt]

1. Vaya a [!DNL samples/browserify/ui-framework/build].
1. Ejecute los mismos comandos que en el paso 2.

Con esta configuración completada, puede continuar con la creación de aplicaciones TVSDK compatibles con Browserify basadas en los ejemplos proporcionados con TVSDK.
