---
description: El SDK de explorador admite actualmente la reproducción de flujos en los que los manifiestos y fragmentos no contienen extensiones.
seo-description: El SDK de explorador admite actualmente la reproducción de flujos en los que los manifiestos y fragmentos no contienen extensiones.
seo-title: Flujos sin extensión
title: Flujos sin extensión
uuid: c69ba62b-a940-4211-920d-2e559849fd6d
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Flujos sin extensión{#extensionless-streams}

El SDK de explorador admite actualmente la reproducción de flujos en los que los manifiestos y fragmentos no contienen extensiones.

## Nivel de fragmento {#section_0E035129501D4A77BBC14192D8A53A86}

El explorador TVSDK analiza los primeros bytes de la respuesta para detectar el tipo de contenido de fragmentos sin extensión. Si no se detecta ningún tipo de contenido válido, TVSDK del explorador generará un error.

## Nivel de manifiesto {#section_AAD9EBAC883D4CC3A0133A45B555EECF}

El SDK de explorador utiliza el `mediaResource.resourceType` parámetro que se pasa en el `replaceCurrentResource` método para detectar el tipo de contenido de la URL de manifiesto. Para obtener más información, consulte la `AdobePSDK.MediaPlayer` clase.

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

Si no `resourceType` se proporciona, la interfaz de usuario determina el tipo de recurso de la extensión URL del recurso, que luego se pasa al `replaceCurrentResource` método .

>[!TIP]
>
>En el caso de los manifiestos sin extensión, asegúrese de que siempre `resourceType` se pasan al cargar un recurso en la interfaz de usuario.

