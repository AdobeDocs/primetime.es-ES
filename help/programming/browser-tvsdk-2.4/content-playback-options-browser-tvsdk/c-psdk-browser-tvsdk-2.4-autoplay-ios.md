---
description: 'null'
seo-description: 'null'
seo-title: Reproducción automática en iOS
title: Reproducción automática en iOS
uuid: d15bad24-be50-49e5-90f4-68dbda96fb6d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Reproducción automática en iOS{#autoplay-on-ios}

La implementación de la API de volumen de AdobePSDK.MediaPlayer permite la reproducción automática del contenido en dispositivos con iOS versión 10 o posterior. iOS solo permite la reproducción automática cuando el volumen está silenciado. Cuando el volumen se establece en cero, la API establece la `muted` propiedad de la etiqueta de vídeo en `true`; de lo contrario, la `muted` propiedad se establece en `false`. La `play` API inicia la reproducción sin ninguna interacción del usuario ni ningún gesto del usuario.

Para la reproducción automática en iPhone, defina además la `playsInline` propiedad de la `video` etiqueta en `true`.

```
videoDiv.getElementsByTagName('video')[0].playsInline = true;
```

>[!NOTE]
>
>El uso de `playsInline` propiedad inicia la reproducción sin el modo de pantalla completa.

