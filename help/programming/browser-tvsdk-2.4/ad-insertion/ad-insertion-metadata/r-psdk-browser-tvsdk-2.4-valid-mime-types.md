---
description: Una publicidad puede tener varios elementos creativos, de los cuales uno se selecciona para reproducirse.
title: Tipos de mime válidos
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# Tipos de mime válidos{#valid-mime-types}

Una publicidad puede tener varios elementos creativos, de los cuales uno se selecciona para reproducirse.

Con los tipos de mime, puede especificar qué tipo de creativo pueden priorizar los usuarios. Los tipos de mime especificados por los usuarios y los tipos de mime compatibles con el TVSDK del explorador se utilizan para determinar qué creativo tendrá prioridad.

Para establecer los tipos de mime válidos en el TVSDK del explorador:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var mimeTypes = [“video/mp4”, “application/x-mpegURL”]; 
auditudeSettings.validMimeTypes = mimeTypes; 
```

donde `mimeTypes` es una matriz de cadenas y cada cadena representa un tipo mime.

En caso de que se devuelvan varios archivos multimedia para un anuncio, la selección depende del orden en que aparezcan los archivos multimedia en la matriz `validMimeTypes`. A los tipos mime que tienen un índice más bajo se les da preferencia sobre los que tienen un índice más alto.
