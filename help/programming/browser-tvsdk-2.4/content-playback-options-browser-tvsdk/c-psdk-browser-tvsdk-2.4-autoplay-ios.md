---
title: Reproducción automática en iOS
description: Reproducción automática en iOS
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '93'
ht-degree: 0%

---

# Reproducción automática en iOS{#autoplay-on-ios}

La implementación de la API por volumen de AdobePSDK.MediaPlayer permite la reproducción automática de contenido en dispositivos con iOS versión 10 o superior. iOS solo permite la reproducción automática cuando el volumen está silenciado. Cuando el volumen está establecido en cero, la API establece el `muted` propiedad de la etiqueta de vídeo para `true`, de lo contrario, `muted` La propiedad se establece en `false`. El `play` La API de inicia la reproducción sin ninguna interacción ni gestos del usuario.

Para la reproducción automática en iPhone, configure además la `playsInline` propiedad del `video` etiqueta a `true`.

```
videoDiv.getElementsByTagName('video')[0].playsInline = true;
```

>[!NOTE]
>
>Uso de `playsInline` inicia la reproducción sin el modo de pantalla completa.
