---
description: Para utilizar Flash Player, asegúrese de que su entorno cumple los requisitos necesarios.
seo-description: Para utilizar Flash Player, asegúrese de que su entorno cumple los requisitos necesarios.
seo-title: Requisitos de Flash Player
title: Requisitos de Flash Player
uuid: f181457b-2bb4-4baa-b2b7-d787f65fab75
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Requisitos de Flash Player{#flash-player-requirements}

Para utilizar Flash Player, asegúrese de que su entorno cumple los requisitos necesarios.

<!--<a id="section_FEE654D506EC4D85AE77302AD2A27777"></a>-->

Estos son los requisitos para Flash Player:

* Para reproducir con `Primetime.js`, instale al menos Flash Player versión 23.
* Para que se le soliciten actualizaciones de Flash Player versión 23 o posterior, instale al menos la versión 11.0.0 de Flash Player.

## Requisitos de empaquetado {#section_F95FC1FEEFEA44D28C9596D2F359AFC7}

La reproducción con Flash Player requiere los siguientes archivos SWF:

* El archivo SWF de la aplicación principal que gestiona las API de TVSDK del explorador.
* El archivo `playerProductInstall.swf` SWF que gestiona la instalación y las actualizaciones de Flash Player.

Además, la reproducción de vídeo en Flash requiere un archivo de token de autorización que puede ser un archivo SWF o un `.DAT` archivo. La ruta a los archivos SWF, el archivo del token de autorización y el nombre y tipo del archivo del token se pueden especificar mediante las API de AdobePSDK.

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

