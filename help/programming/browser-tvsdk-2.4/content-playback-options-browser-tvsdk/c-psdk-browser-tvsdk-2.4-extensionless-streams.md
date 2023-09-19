---
description: TVSDK del explorador admite actualmente la reproducción de secuencias en las que manifiestos y fragmentos no contienen extensiones.
title: Flujos sin extensión
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# Flujos sin extensión{#extensionless-streams}

TVSDK del explorador admite actualmente la reproducción de secuencias en las que manifiestos y fragmentos no contienen extensiones.

## Nivel de fragmento {#section_0E035129501D4A77BBC14192D8A53A86}

TVSDK del explorador analiza los primeros bytes de la respuesta para detectar el tipo de contenido de los fragmentos sin extensión. Si no se detecta ningún tipo de contenido válido, TVSDK del explorador generará un error.

## Nivel de manifiesto {#section_AAD9EBAC883D4CC3A0133A45B555EECF}

El TVSDK del explorador utiliza `mediaResource.resourceType` parámetro que se pasa en el `replaceCurrentResource` para detectar el tipo de contenido de la URL del manifiesto. Para obtener más información, consulte la `AdobePSDK.MediaPlayer` clase.

En el reproductor del marco de trabajo de la interfaz de usuario, puede especificar el tipo de recurso en el recurso de medios de la siguiente manera:

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

If `resourceType` no se proporciona, el marco de trabajo de la interfaz de usuario determina el tipo de recurso de la extensión URL de recurso, que se pasa a `replaceCurrentResource` método.

>[!TIP]
>
>Para el manifiesto sin extensión, asegúrese de que `resourceType` siempre se pasa al cargar un recurso en el marco de trabajo de la interfaz de usuario.
