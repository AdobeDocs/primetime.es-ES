---
description: Para utilizar el Flash Player, asegúrese de que su entorno cumpla los requisitos necesarios.
title: requisitos de Flash Player
exl-id: 26531d0d-d34c-4134-8a05-0604f00a3107
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# requisitos de Flash Player{#flash-player-requirements}

Para utilizar el Flash Player, asegúrese de que su entorno cumpla los requisitos necesarios.

<!--<a id="section_FEE654D506EC4D85AE77302AD2A27777"></a>-->

Estos son los requisitos para el Flash Player:

* Para reproducir con `Primetime.js`, instale al menos la versión 23 de Flash Player.
* Para que se le soliciten actualizaciones para la versión de Flash Player 23 o posterior, instale al menos la versión de Flash Player 11.0.0.

## Requisitos de empaquetado {#section_F95FC1FEEFEA44D28C9596D2F359AFC7}

La reproducción con Flash Player requiere los siguientes archivos de SWF:

* Archivo del SWF de aplicaciones principal que administra las API de TVSDK del explorador.
* El `playerProductInstall.swf` Archivo del SWF que gestiona la instalación y las actualizaciones del Flash Player.

Además, la reproducción de vídeo en Flash requiere un archivo de token de autorización que puede ser un SWF o un `.DAT` archivo. La ruta a los archivos del SWF, el archivo del token de autorización, el nombre y el tipo del archivo del token se pueden especificar mediante las API de AdobePSDK.

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
