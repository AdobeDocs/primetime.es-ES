---
description: Un anuncio puede tener varios elementos creativos, de los cuales se selecciona uno para reproducirlo.
title: Tipos MIME válidos
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# Tipos MIME válidos{#valid-mime-types}

Un anuncio puede tener varios elementos creativos, de los cuales se selecciona uno para reproducirlo.

Con los tipos MIME, puede especificar qué tipo creativo pueden priorizar los usuarios. Los tipos MIME especificados por los usuarios y los tipos MIME admitidos por el TVSDK del explorador se utilizan para determinar qué creativo se priorizará.

Para establecer los tipos MIME válidos en el explorador TVSDK:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var mimeTypes = [“video/mp4”, “application/x-mpegURL”]; 
auditudeSettings.validMimeTypes = mimeTypes; 
```

donde `mimeTypes` es una matriz de cadenas y cada cadena representa un tipo mime.

Si se devuelven varios archivos multimedia para un anuncio, la selección depende del orden en que aparezcan los archivos multimedia en `validMimeTypes` matriz. Los tipos MIME con un índice más bajo tienen preferencia sobre los que tienen un índice más alto.
