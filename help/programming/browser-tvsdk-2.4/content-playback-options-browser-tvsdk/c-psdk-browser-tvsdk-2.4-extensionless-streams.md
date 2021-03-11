---
description: El SDK de explorador admite actualmente la reproducción de flujos en los que los manifiestos y fragmentos no contienen extensiones.
title: Flujos sin extensión
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---


# Flujos sin extensión{#extensionless-streams}

El SDK de explorador admite actualmente la reproducción de flujos en los que los manifiestos y fragmentos no contienen extensiones.

## Nivel de fragmento {#section_0E035129501D4A77BBC14192D8A53A86}

El explorador TVSDK analiza los primeros bytes de la respuesta para detectar el tipo de contenido de fragmentos sin extensión. Si no se detecta ningún tipo de contenido válido, el SDK de TVSDK del explorador generará un error.

## Nivel de manifiesto {#section_AAD9EBAC883D4CC3A0133A45B555EECF}

El SDK de TVSDK del explorador utiliza el parámetro `mediaResource.resourceType` que se pasa en el método `replaceCurrentResource` para detectar el tipo de contenido de la dirección URL del manifiesto. Para obtener más información, consulte la clase `AdobePSDK.MediaPlayer` .

En el reproductor de interfaz de usuario de Framework, puede especificar el tipo de recurso en el recurso de medios de la siguiente manera:

```js
var playerWrapper = ptp.videoPlayer('.videoDiv', { 
  player: { 
    mediaResource: { 
      resourceUrl:'Specify Resource Url', 
      resourceType: ‘Specify Resource Type. Refer AdobePSDK.MediaResourceType' 
    } 
  } 
}); 
```

Si no se proporciona `resourceType`, el marco de interfaz de usuario determina el tipo de recurso de la extensión URL del recurso, que luego se pasa al método `replaceCurrentResource`.

>[!TIP]
>
>Para el manifiesto sin extensión, asegúrese de que `resourceType` siempre se pase al cargar un recurso en el marco de la interfaz de usuario.

