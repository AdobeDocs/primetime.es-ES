---
description: Puede crear un reproductor compatible con Browserify utilizando los archivos JS proporcionados por el TVSDK del explorador.
title: Reproductor compatible con Browserify
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Información general {#browserify-compatible-player-overview}

Puede crear un reproductor compatible con Browserify utilizando los archivos JS proporcionados por el TVSDK del explorador.

El TVSDK del explorador proporciona dos archivos JS compatibles con Browserify. Una es para uso con el módulo AdobePSDK; esto es para desarrollar aplicaciones sin el marco de IU. El otro es para uso con el módulo UI-Framework; devuelve el espacio de nombres PTP que utiliza para escribir aplicaciones mediante el marco de IU.

Para comenzar con Browserify, ejecute los siguientes comandos de configuración para crear [!DNL final.js] archivos (su archivo de paquete Browserify) dentro de los directorios [!DNL example] en [!DNL samples/browerify/reference] y [!DNL samples/browerify/ui-framework]:

1. Vaya a [!DNL samples/browserify/reference/build].
1. Ejecute los siguientes comandos:

   1. [!DNL npm install]
   1. [!DNL node_modules/.bin/grunt]

1. Vaya a [!DNL samples/browserify/ui-framework/build].
1. Ejecute los mismos comandos que en el paso 2.

Con esta configuración finalizada, puede continuar creando aplicaciones TVSDK compatibles con Browserify basadas en los ejemplos proporcionados con TVSDK.
