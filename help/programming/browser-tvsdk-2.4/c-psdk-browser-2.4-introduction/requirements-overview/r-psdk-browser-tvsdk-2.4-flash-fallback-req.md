---
description: Para utilizar el Flash Player, asegúrese de que su entorno cumpla los requisitos necesarios.
title: requisitos de Flash Player
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 1%

---


# Requisitos de Flash Player{#flash-player-requirements}

Para utilizar el Flash Player, asegúrese de que su entorno cumpla los requisitos necesarios.

<!--<a id="section_FEE654D506EC4D85AE77302AD2A27777"></a>-->

Estos son los requisitos para el Flash Player:

* Para reproducir con `Primetime.js`, instale al menos la versión 23 del Flash Player.
* Para que se le soliciten actualizaciones de la versión 23 o posterior del Flash Player, instale al menos la versión 11.0.0 del Flash Player.

## Requisitos de paquete {#section_F95FC1FEEFEA44D28C9596D2F359AFC7}

La reproducción con Flash Player requiere los siguientes archivos SWF:

* El archivo SWF de la aplicación principal que gestiona las API de TVSDK del explorador.
* El archivo SWF `playerProductInstall.swf` que gestiona la instalación y las actualizaciones del Flash Player.

Además, la reproducción de vídeo en Flash requiere un archivo de token de autorización que puede ser un archivo SWF o `.DAT`. La ruta a los archivos SWF, el archivo del token de autorización y el nombre y tipo del archivo del token se pueden especificar mediante las API de AdobePSDK.

Por ejemplo:

```js
// Set relative or http path to directory containing SWF.  
// Defaults to current directory for the html page. 
AdobePSDK.setSWFPath(<swfPath>); 
 
// Set the relative or http path to directory containing token file(s). 
// Defaults to SWFPath + "token/". 
AdobePSDK.setAuthorizationTokenPath(<authorizationTokenPath>); 
 
// Set the name of the token file, do not include any path in this string. 
AdobePSDK.setAuthorizationTokenFilename("hlsaf_localhost.swf"); 
 
//Set the token type, "DAT" or "SWF". Defaults to "DAT" 
AdobePSDK.setAuthorizationTokenType("SWF");
```

