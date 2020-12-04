---
description: Puede crear un reproductor compatible con Browserify mediante archivos JS proporcionados por el TVSDK del explorador.
seo-description: Puede crear un reproductor compatible con Browserify mediante archivos JS proporcionados por el TVSDK del explorador.
seo-title: Reproductor compatible con Browserify
title: Reproductor compatible con Browserify
uuid: 1832c826-d5d0-41b0-852f-286c8e4fa0f3
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---


# Información general {#browserify-compatible-player-overview}

Puede crear un reproductor compatible con Browserify mediante archivos JS proporcionados por el TVSDK del explorador.

TVSDK del explorador proporciona dos archivos JS compatibles con Browserify. Una se utiliza con el módulo AdobePSDK; esto es para desarrollar aplicaciones sin el marco de interfaz de usuario. El otro se utiliza con el módulo UI-Framework; devuelve la Área de nombres PTP que se utiliza para escribir aplicaciones mediante la interfaz de usuario de Framework.

Para comenzar con Browserify, ejecute los siguientes comandos de configuración para crear [!DNL final.js] archivos (el archivo de paquete Browserify) dentro de los directorios [!DNL example] en [!DNL samples/browerify/reference] y [!DNL samples/browerify/ui-framework]:

1. Vaya a [!DNL samples/browserify/reference/build].
1. Ejecute los siguientes comandos:

   1. [!DNL npm install]
   1. [!DNL node_modules/.bin/grunt]

1. Vaya a [!DNL samples/browserify/ui-framework/build].
1. Ejecute los mismos comandos que en el paso 2.

Con esta configuración finalizada, puede crear aplicaciones TVSDK compatibles con Browserify basándose en los ejemplos proporcionados con el TVSDK.
