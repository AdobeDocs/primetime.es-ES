---
description: Una publicidad puede tener varios elementos creativos, de los cuales uno se selecciona para reproducirse.
seo-description: Una publicidad puede tener varios elementos creativos, de los cuales uno se selecciona para reproducirse.
seo-title: Tipos de mime válidos
title: Tipos de mime válidos
uuid: ab2baac9-a9ef-44f1-83a1-2e6e471e3231
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Tipos de mime válidos{#valid-mime-types}

Una publicidad puede tener varios elementos creativos, de los cuales uno se selecciona para reproducirse.

Con los tipos de MIME, puede especificar qué tipo de elemento creativo pueden priorizar los usuarios. Los tipos de MIME especificados por los usuarios y los tipos de MIME admitidos por el SDK de TVSDK de explorador se utilizan para determinar qué elemento creativo se priorizará.

Para definir los tipos de MIME válidos en el SDK de TVSDK del explorador:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var mimeTypes = [“video/mp4”, “application/x-mpegURL”]; 
auditudeSettings.validMimeTypes = mimeTypes; 
```

donde `mimeTypes` es una matriz de cadenas y cada cadena representa un tipo de MIME.

En caso de que se devuelvan varios archivos de medios para una publicidad, la selección depende del orden en que los archivos de medios aparezcan en la `validMimeTypes` matriz. A los tipos MIME que tienen un índice más bajo se les da una preferencia sobre los que tienen un índice más alto.
